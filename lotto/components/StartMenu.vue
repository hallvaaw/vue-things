<template>
    <main class="max-w-6xl mx-auto p-6">
        <section class="flex flex-row justify-between">
            <img :src="duckImage" class="rounded w-1/4 h-64 hover:w-1/3 hover:h-72 ease-in duration-150" alt="">
            <img :src="dogImage"  class="rounded w-1/4 h-64 hover:w-1/3 hover:h-72 ease-in duration-150" alt="">
            <img :src="foxImage"  class="rounded w-1/4 h-64 hover:w-1/3 hover:h-72 ease-in duration-150" alt="">
        </section>
    </main>
</template>

<script>
export default {
    name: 'StartMenu',
    data() {
        return {
            duckImage: 'https://random-d.uk/api/152.jpg',
            dogImage: 'https://random.dog/1800eefa-6a30-48b8-9c3f-ad1eb6fd9abe.jpg',
            foxImage: 'https://randomfox.ca/images/90.jpg'
        }
    }
}
</script>

