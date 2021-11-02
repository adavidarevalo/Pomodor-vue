<template>
    <section>
        <button
        @click="changeSound()"
        v-if='soundActive'
        ><sound/></button>
        <button
        v-else
        @click="changeSound()"
        ><noSound/></button>
        <p>{{minutes}}:{{seconds}}</p>
        <button
        @click="changeButton()"
        v-if="!startButton"
        >start</button>
        <button
        v-else
        @click="changeButton()"
        >resume</button>
        <button
        style="margin: 15px 0px 0px"
        @click='reloadCLick()'
        >
            <reload/>
        </button>
    </section>
</template>


<script>
import sound from '@/assets/sound.vue'
import noSound from '@/assets/noSound.vue'
import reload from '@/assets/reload.vue'

//Sounds
let  audioFinished = new Audio(require('../assets/sounds/timesUp.mp3'))
let  audioStart = new Audio(require('../assets/sounds/startTimer.mp3'))
let  audioPause = new Audio(require('../assets/sounds/pauseTimer.mp3'))
let  audioSlide = new Audio(require('../assets/sounds/slide.mp3'))
export default{
    name: 'Clock',
    props: [
        'count'
    ],
    components: {
        sound,
        noSound,
        reload
    },
    data(){
        return{
            startButton: false,
            soundActive: true,
            minutes: 15,
            seconds: 0
        }
    },
    watch: {
        count:function (count) {
            this.startButton = false
            this.minutes = count
            this.seconds = 0
            console.log('minutesx2 ', count)
            console.log('minutes ', this.minutes)
        }
    },
    methods: {
        changeButton(){
            this.startButton = !this.startButton
            audioFinished.pause()
            if(this.startButton){
                audioStart.play()
                this.CountDown();
            } else {
                audioPause.play()
            }
        },
        reloadCLick(){
            audioSlide.play()
        },
        changeSound(){
            audioSlide.play()
            this.soundActive = !this.soundActive
        },
        CountDown: function () {
        this.interval = setInterval(()=>{
            if(this.seconds === 0 && this.minutes === 0 || !this.startButton){
                clearTimeout(this.interval)
                if(!this.startButton){
                    console.log('Pause...')
                    return
                } 
                this.startButton = false
                audioFinished.play()
            } else if(this.seconds === 0){
                this.seconds = 59
                this.minutes = this.minutes - 1
            } else {
                this.seconds = this.seconds - 1
            }
        }, 1000)  
            }
        },
    }
</script>
<style scoped>
section{
    border-radius: 50%;
    background: linear-gradient(145deg, #15172d, #191b36);
    box-shadow:  50px 50px 100px #090a14,
                -50px -50px 100px #252850;
    width: 250px;
    height: 250px;
    margin: 0 auto;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
}
p{
    color: #D7E0FF;
    font-size: 4rem;
    font-weight: 500;
    letter-spacing: 3px;
    margin: 0px;
}
button{
    color: #D7E0FF;
    border: none;
    background: none;
    text-transform: uppercase;
    font-size: 1.4rem;
    letter-spacing: 5px;
    cursor: pointer;
}
</style>