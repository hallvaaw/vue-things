<template>
    <main class="max-w-6xl mx-auto p-6">
        <div v-if="newGame == true" :class="newGame == false ? 'hidden' : ''">
            <StartMenu @animal-selection="(selection) => animalSelection = (selection)" @click="renderSelection()"/>
        </div>
            <section v-if="showReplayScreen == false" class="grid grid-cols-4 gap-1">
                <div v-for="pic in pictures" class="flex justify-center items-center bg-gray-800 rounded hover:bg-gray-700 active:bg-gray-600" :class="pic.pair === true ? 'border-6 border-gray-50 bg-gray-50 hover:bg-gray-50 active:bg-gray-50' : ''">
                    <img :src="pic.img" alt="" @click="revealImage(pic)" class="rounded w-72 h-56" :class="[pic.open === true ? 'opacity-100 cursor-not-allowed pointer-events-none' : 'opacity-0 transition delay-500', pic.pair === true ? 'w-64 h-52 ease-in duration-100' : '']">
                </div>
            </section>
        <img v-else @click="startNewGame()" src="./assets/replay_screen.png" alt="" class="w-full h-full ease-in duration-100">
    </main>
</template>

<script>
import StartMenu from './components/StartMenu.vue'
import JSConfetti from 'js-confetti'

const confetti = new JSConfetti()

let selectionArray = []
let correctImages = 0
let timeDelay = 500

function shuffle(inputArray) {
    let currentIndex = inputArray.length,  randomIndex;

    while (currentIndex != 0) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex--;

        [inputArray[currentIndex], inputArray[randomIndex]] = [
            inputArray[randomIndex], inputArray[currentIndex]
        ];
}
  return inputArray;
}

export default {
    name: 'App',
    components: {
        StartMenu
    },
    data() {
        return {
            pictures: [],
            showReplayScreen: false,
            newGame: true,
            animalSelection: ''
        }
    },
    methods: {
        async getDuck() {
            const duckRes = await fetch('http://localhost:8080/random-d.uk/api/list')
            const duckImages = await duckRes.json()
            for (let i = 0; i < 6; i++) {
                let randomNum = Math.floor(Math.random() * 285)
                this.pictures.push({id: randomNum, img: `https://random-d.uk/api/${duckImages.images[randomNum]}`, open: false, pair: false})
                this.pictures.push({id: randomNum, img: `https://random-d.uk/api/${duckImages.images[randomNum]}`, open: false, pair: false})
            }

            shuffle(this.pictures)
            this.newGame = false
        },
        async getDog() {
            const dogRes = await fetch('http://localhost:8080/random.dog/doggos')
            const dogFiles = await dogRes.json()
            const dogImages = dogFiles.filter(img => img.includes('.jpg'))
            for (let i = 0; i < 6; i++) {
                let randomNum = Math.floor(Math.random() * dogImages.length)
                this.pictures.push({id: randomNum, img: `https://random.dog/${dogImages[randomNum]}`, open: false, pair: false})
                this.pictures.push({id: randomNum, img: `https://random.dog/${dogImages[randomNum]}`, open: false, pair: false})
            }

            shuffle(this.pictures)
            this.newGame = false
        },
        async getFox() {
            for (let i = 0; i < 6; i++) {
                let foxRes = await fetch('http://localhost:8080/randomfox.ca/floof')
                let foxImages = await foxRes.json()
                let randomNum = Math.floor(Math.random() * 122)
                this.pictures.push({id: randomNum, img: `${foxImages.image}`, open: false, pair: false})
                this.pictures.push({id: randomNum, img: `${foxImages.image}`, open: false, pair: false})
            }

            shuffle(this.pictures)
            this.newGame = false
        },
        revealImage(e) {
            e.open = true
            selectionArray.push(e)
            if (selectionArray.length == 2) {
                if (selectionArray[0].id == selectionArray[1].id) {
                    selectionArray[0].pair = true
                    selectionArray[1].pair = true
                    selectionArray = []
                    correctImages += 1
                } else {
                    setTimeout(function() {
                        for (let i = 0; i < selectionArray.length; i++) {
                            selectionArray[i].open = false
                        }
                        selectionArray = []}, timeDelay)
                }
            }
            if (correctImages == 6) {
                confetti.addConfetti()
                this.showReplayScreen = true
            }
        },
        startNewGame() {
            location.reload()
        },
        renderSelection() {
            if (this.animalSelection == 'duck') {
                this.getDuck()
            } else if (this.animalSelection == 'dog') {
                this.getDog()
            } else if (this.animalSelection == 'fox') {
                this.getFox()
            }
        }
    }
}
</script>

