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
        <p>{{minutes}} : {{seconds}}</p>
        <button
        @click="changeButton()"
        v-if="!startButton"
        >start</button>
        <button
        v-else
        @click="changeButton()"
        >resume</button>
    </section>
</template>


<script>
import sound from '@/assets/sound.vue'
import noSound from '@/assets/noSound.vue'

export default{
    name: 'Clock',
    components: {
        sound,
        noSound
    },
    data(){
        return{
            startButton: false,
            soundActive: true,
            numberClock: 15,
            minutes: 1,
            seconds: 0
        }
    },
    methods: {
        changeButton(){
            this.startButton = !this.startButton
            if(this.startButton){
                console.log('Play baby')
                this.CountDown();
            }
        },
        changeSound(){
            this.soundActive = !this.soundActive
        },
        clockElement(number = 15){
            setTimeout(() => {
                this.numberClock = number - 1
            }, 1000);
        },
        CountDown: function () {
        this.interval = setInterval(()=>{
            if(this.seconds === 0 && this.minutes === 0 || !this.startButton){
                console.log('Terminado...')
                clearTimeout(this.interval)
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