<template>
    <section v-show="modal">
        <div class="Modal-Container">
            <form  @submit="sendInformation">
                <div class="Form-header">
                    <h2>Settings</h2>
                    <button @click='CloseModal()'><Close/></button>
                </div>
                <div class="Modal-time">
                    <h3>Time (minutes)</h3>
                    <div>
                        <label>pomodoro</label>
                        <input 
                        type='number' 
                        v-model='formContainer.pomodoro'
                        min="1" 
                        max="59"
                        />
                    </div>
                    <div>
                        <label>short break</label>
                        <input 
                        type='number' 
                        min="1" 
                        max="59"
                        v-model='formContainer.shortbreak'
                        />
                    </div>
                    <div>
                        <label>long break</label>
                        <input 
                        type='number' 
                        min="1" 
                        max="59"
                        v-model='formContainer.longbreak'
                        />
                    </div>
                </div>
                <div class="Modal-Font">
                    <h3>Font</h3>
                    <div>
                        <div
                        @click='changeFont(1, "Arial")'
                        v-bind:class="{fontActive: font === 1}"
                        >Aa</div>
                        <div
                        @click='changeFont(2, "Roboto")'
                        v-bind:class="{fontActive: font === 2}"
                        >Aa</div>
                        <div
                        @click='changeFont(3, "Time New Roman")'
                        v-bind:class="{fontActive: font === 3}"
                        >Aa</div>
                    </div>
                </div>
                <div class="Modal-Color">
                    <h3>color</h3>
                    <div>
                        <div
                        @click='changeColor(1, "#F87070")'
                        v-bind:class="{colorActive: color === 1}"
                        style="background: #F87070;"></div>
                        <div 
                        @click='changeColor(2, "#70F3F8")'
                        v-bind:class="{colorActive: color === 2}"
                        style="background: #70F3F8;"></div>
                        <div
                        @click='changeColor(3, "#D881F8")'
                        v-bind:class="{colorActive: color === 3}"
                        style="background: #D881F8;"></div>
                    </div>
                </div>
                <input type='submit' value='Apply' class="Submit"/>
            </form>
        </div>
    </section>
</template>

<script>

import Close from '../assets/close.vue'
let  audioSlide = new Audio(require('../assets/sounds/slide.mp3'))

export default{
    name: 'Modal',
    props: [
        'modalContainer',
        'sound'
    ],
    components: {
        Close
    },
    data(){
        return{
            modal: false,
            color: 1,
            font: 1,
            formContainer: {
                pomodoro: 25,
                shortbreak: 5,
                longbreak: 15,
                font: 'Arial',
                color: '#F87070'
            },
            soundElement: true
        }
    },
    watch:{
        modalContainer: function(modalValue) { 
            this.modal = modalValue
        },
        sound: function (soundValue) {
            this.soundElement = soundValue
        }
    },
    methods: {
        CloseModal(){
            this.modal = false
            this.$emit('close',false);
        },
        sendInformation: function (e) {
            this.$emit('data',this.formContainer);
            e.preventDefault();
            this.soundFm()
            this.CloseModal()
        },
        changeColor(number, color){
            this.soundFm()
            this.color = number,
            this.formContainer.color = color
        },
        changeFont(number, font){
            this.soundFm()
            this.font = number
            this.formContainer.font = font
        },
        soundFm(){
            if(this.soundElement){
                audioSlide.play()
            }
        }
    }
}
</script>

<style scoped>
section{
    width: 100%;
    position: fixed;
    left: 0px;
    top: 0px;
    height: 100vh;
    background: #0000006b;
    display: flex;
    justify-content: center;
    align-items: center;
}

button{
    background: none;
    border: none;
}
.Modal-Container{
    width: 90%;
    border-radius: 5px;
    background: white;
    max-width: 500px;
    animation: fadeInUp 1s both;
}
.Form-header{
    display: flex;
    justify-content: space-around;
    align-items: center;
    border-bottom: 1px solid #80808061;
}
h2{
    font-weight: 800;
    letter-spacing: 2px;
    margin-bottom: 10px;
}
h3{
    text-transform: uppercase;
}
.Modal-time{
    border-bottom: 1px solid #80808061;
}
.Modal-time > div{
    width: 80%;
    display: flex;
    justify-content: space-between;
    margin: 15px auto;
}
label{
    font-weight: 600;
    letter-spacing: 1px;
}
input{
    background: #EEF1FA;
    border: none;
    border-radius: 25px;
    padding: 5px 15px;
    width: 50px;
    width: 80px;
    color: black;
}
.Modal-Font{
    border-bottom: 1px solid #80808061;
}
.Modal-Font > div{
    display: flex;
    width: 80%;
    margin: 0 auto 15px;
    justify-content: space-between;
}
.Modal-Font > div > div{
    background: #EEF1FA;
    border-radius: 50%;
    font-size: 1rem;
    width: 45px;
    height: 45px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
}
.Modal-Color > div{
    display: flex;
    width: 80%;
    margin: 0 auto;
    justify-content: space-between;
}
.Modal-Color > div >div{
    border-radius: 50%;
    font-size: 1rem;
    width: 45px;
    height: 45px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
}
.Submit{
    font-size: 1rem;
    font-weight: 600;
    padding: 10px 20px;
    text-align: center;
    background: #F87070;
    color: white;
    position: relative;
    top: 20px;
    cursor: pointer;
}
.Submit:hover,
.Submit:active{
    transform: scale(1.1);
}
.colorActive{
    background-image: url('../assets/check.svg') !important;
    background-position: center !important;
    background-size: cover !important;
}
.fontActive{
    background: #1F213F !important;
    color: white;
}
  @keyframes fadeInUp {
  0% {
  opacity: 0;
  transform: translate3d(0, 100%, 0);
  }
  100% {
  opacity: 1;
  transform: none;
  }
  } 
</style>