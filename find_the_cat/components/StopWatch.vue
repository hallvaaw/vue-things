<template>
  <div>
    <p class="text-4xl tracking-wide">{{ minutes }}:{{ seconds }}</p>
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
        timeDisplay() {
            setInterval(() => {
                this.seconds++
                if (this.seconds < 10) {
                    this.seconds = "0" + this.seconds
                }
                if (this.seconds == 60) {
                    this.minutes++
                    if (this.minutes < 10) {
                        this.minutes = "0" + this.minutes
                    }
                    this.seconds = 0
                }
            }, 1000)
        }
    }
}
</script>
