<template>
    <main class="container relative mx-auto">
        <h1 class="text-gray-200 text-5xl text-center">Find the cat</h1>
            <!--img :src="'./assets/' + pictures[2].img" alt="Cat" /-->
            <div class="items-center">
                <img :src="pictures[selectedPicture].img" alt="Cat" style=pictures[selectedPicture].imageHeight; />
            </div>
            <p class="absolute bottom-[90px] text-green-200">Source: {{ pictures[1].imageSource }}</p>
            <div class="text-center">
                <button @click="nextClick()" class="rounded text-2xl text-white font-bold py-2 px-4" :class="win == true ? 'bg-green-600': 'text-gray-400 bg-blue-600'">Next</button>
                <stopwatch :running="running" :resetWhenStart="true" />
            </div>
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
            pictures: [
                {img: "src/assets/0.jpeg", xOffSet: "", yOffSet: "", imageHeight: "height: 700px;", imageWidth: "650px", imageSource: "u/pizzaslayer111"},
                {img: "src/assets/1.jpg", xOffSet: "", yOffSet: "", imageSource: "@katehinds"},
                {img: "src/assets/2.jpg", xOffSet: "", yOffSet: "", imageSource: "u/waterhauler"},
                {img: "src/assets/3.jpg", xOffSet: "", yOffSet: "", imageSource: "@thereisnocat"},
                {img: "src/assets/4.jpg", xOffSet: "", yOffSet: "", imageSource: "@ltlindian2"}

            ],
            selectedPicture: 0,
            correctTile: false,
            win: false
        }
    },
    methods: {
        tileClick(e) {
            if (e.tileId == this.pictures[0].correctTiles) {
                this.running = false
                this.win = true
            }
        },
        nextClick() {
            this.selectedPicture++
            this.win = false
            this.seconds = 0
            this.minutes = 0
            this.running = true
        }
    }
}
</script>
