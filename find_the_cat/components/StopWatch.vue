<template>
  <div>
    <p>{{ minutes }}</p>
    <p>{{ seconds }}</p>
  </div>
</template>

<script>
export default {
    name: "stopwatch",
    props: {
        running: {
            type: Boolean,
            default: false
        }
    },
    mounted() {
        this.timeDisplay()
    },
    data() {
        return { 
            seconds: 0,
            minutes: 0
        }
    },
    methods: {
        startTime() {
            this.seconds++
            if (this.seconds == 60) {
                this.minutes++
                this.seconds = 0
            }
        },
        timeDisplay() {
            setInterval(() => {
                this.seconds++
                if (this.seconds == 60) {
                    this.minutes++
                    this.seconds = 0
                }
            }, 1000)
        }
    }
}
</script>
