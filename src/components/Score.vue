<template>
    <div id="score">
        <p id="details">{{ clickvar.details }}</p>
        <p class="span-results">
            <b>Your High Score</b>
            <p id="highscore">{{ clickvar.highscore }}</p>
        </p>
    </div>
    </template>
    
    <script>
    export default {
        data() {
            return {}
        },
        props: {
            clickvar: Object
        }
    }
    </script>