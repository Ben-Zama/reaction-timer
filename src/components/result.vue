<template>
  <p class="reaction">Your reaction time is: {{ score }}<span>ms</span> </p>
  <p class="rank">{{ rank }}</p>
</template>

<script>
export default {
    props: ['score'],
    data() {
        return {
            rank: null
        }
    },
    mounted() {
        if (this.score < 500) {
            this.rank = 'Ligning Fast'
        }
        else if (this.score < 600) {
            this.rank = 'Quick Reflexes'
        }
        else if (this.score < 800) {
            this.rank = 'Average'
        }
        else if (this.score < 1000) {
            this.rank = 'Slow to React'
        } else {
            this.rank = 'Lagging Behind'
        }
    }
}
</script>

<style scoped>
.reaction {
    color: #35495e;
}
.reaction span {
    color: red;
}
.rank {
    color: #40b882;
    font-size: 20px;
    font-weight: bold;
}
</style>