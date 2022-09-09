<template>
    <button class="actionBtn" id="go" v-if="clickvar.show" @click="go()">Go</button>
    <button id="stop" class="actionBtn" v-if="!clickvar.show" @click="stop()">Stop</button>
</template>
<script>
export default {
    data() {
        return {
        }
    },
    props: {
        clickvar: Object
    },
    methods: {
        go() {
            this.clickvar.details = "Pay attention Click stop when the color changes.";
            this.clickvar.show = !this.clickvar.show;
            let interval = Math.floor(Math.random() * (5000 - 2000 + 1) + 2000);
            this.clickvar.timeout = setTimeout(() => {
                this.clickvar.isActive = false;
                this.clickvar.timeStart = new Date().getTime();
            }, interval);
            this.clickvar.timeStart = 0;
        },
        stop() {
            this.clickvar.isActive = true;
            this.clickvar.show = !this.clickvar.show;
            if (this.clickvar.timeStart == 0) {
                this.clickvar.details = "Too quick... Try again!";
                clearTimeout(this.clickvar.timeout);
            } else {
                this.clickvar.timeStop = new Date().getTime();
                this.clickvar.diff = this.clickvar.timeStop - this.clickvar.timeStart;
                this.clickvar.score = (this.clickvar.diff / 1000).toFixed(2);
                if (this.clickvar.firstRun === 1) {
                    this.clickvar.highscore = this.clickvar.score;
                    this.clickvar.firstRun++;
                    this.clickvar.details = `You've set a new high score: ${this.clickvar.highscore} seconds!`;
                } else if (this.clickvar.score < this.clickvar.highscore) {
                    this.clickvar.highscore = this.clickvar.score;
                    this.clickvar.details = `You've set a new high score: ${this.clickvar.highscore} seconds!`;
                } else {
                    this.clickvar.details = `Your time was: ${this.clickvar.score} seconds. Try again!`;
                }
               
            }
        },
    },
}

</script>