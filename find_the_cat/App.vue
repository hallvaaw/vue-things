<template>
    <h1 class="bg-blue-200">Hello world!</h1>
    <main class="container mx-auto">
        <h1 class="text-center">Find the cat</h1>
        <section class="grid grid-cols-6">
            <div class="col-span-2"></div>
            <div class="relative w-[500px]">
                <img src="./assets/display.jpeg" alt="">
                <div v-for="picture in pictures" class="absolute inset-0 grid grid-cols-12">
                    <div v-for="tile in picture.tiles" @click="onClick(tile)" class="bg-blue-200 border-blue-600 p-1 opacity-10 hover:bg-blue-900 cursor-default">&nbsp;</div>
                </div>
            </div>
            <div></div>
        </section>
    </main>
</template>

<script>
export default {
    name: 'App',
    data() {
        return {
            tilesArray: [],
            pictures: [],
            correctTile: false
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
        onClick(e) {
            console.log(e.tileId)
            console.log()
            if (e.tileId == this.pictures[0].correctTiles) {
                console.log("You win!")
            }
        }
    }
}
</script>
