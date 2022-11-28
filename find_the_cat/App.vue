<template>
    <h1 class="bg-blue-200">Hello world!</h1>
    <main class="container mx-auto">
        <h1 class="text-center">Find the cat</h1>
        <section class="grid grid-cols-6">
            <div class="col-span-2"></div>
            <div class="relative w-[500px]">
                <img src="./assets/display.jpeg" alt="">
                <div v-for="picture in pictures" class="absolute inset-0 grid grid-cols-12">
                    <div v-for="tile in picture.tiles" @click="tileClick(tile)" class="bg-blue-200 border-blue-600 p-1 opacity-10 hover:bg-blue-900 cursor-default" :class="win == true ? 'bg-gray-900 opacity-60': ''">&nbsp;</div>
                </div>
            </div>
            <div>
            </div>
                <div>
                    <button @click="nextClick()" class="rounded text-2xl text-white font-bold py-2 px-4" :class="win == true ? 'bg-green-600': 'text-gray-400 bg-blue-600'">Next</button>
                </div>
        </section>
                <stopwatch :running="running" :resetWhenStart="true" />
    </main>
</template>

<script>
import stopwatch from "./components/StopWatch.vue"
export default {
    name: 'App',
    components: {
        stopwatch
    },
    data() {
        return {
            running: true,
            tilesArray: [],
            pictures: [],
            correctTile: false,
            win: false
        }
    },
    mounted() {
        this.addPictures()
        this.addTiles()
    },
    methods: {
        addTiles() {
            for (let i = 0; i < 240; i++) {
                this.tilesArray.push({tileId: i})
            }
        },
        addPictures() {
            this.pictures.push({id: 1, img: "./assets/display.jpeg", tiles: this.tilesArray, correctTiles: 113})
        },
        tileClick(e) {
            if (e.tileId == this.pictures[0].correctTiles) {
                this.running = false
                this.win = true
            }
        },
        nextClick() {
            this.win = false
            this.time = 0
            this.running = true
        }
    }
}
</script>
