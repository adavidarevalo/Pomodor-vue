<template>
    <main>
        <div class="Home-Header">
            <h1>pomodoro</h1>
            <HomeNav 
            :data='data'
            :sound='sound'
            @count='changeMinutes($event)'
            />
        </div>
        <Clock 
        :count='count'
        :colorElement='data'
        @sound='changeSound($event)'
        />
        <button @click="OpenModal()">
            <wheel/>
        </button>
        <Modal 
        :modalContainer='modalContainer' 
        :sound='sound'
        @close='CloseModal($event)' 
        @data='addData($event)'/>
    </main>
</template>

<script>
import HomeNav from '../components/HomeNav.vue'
import Clock from '../components/Clock.vue'
import wheel from '../assets/wheel.vue'
import Modal from '../components/Modal.vue'
//Sound 
let  audioSlide = new Audio(require('../assets/sounds/slide.mp3'))

export default{
    name: 'Home',
    components: {
        HomeNav,
        Clock,
        wheel,
        Modal
    },
    data(){
        return{
            modalContainer: false,
            data: {
                pomodoro: 25,
                shortbreak: 5,
                longbreak: 15,
                font: 'Arial',
                color: '#F87070'
            },
            count: 15,
            sound: true
        }
    },
    methods:{
        OpenModal(){
            if(this.sound){
                audioSlide.play()
            }
            this.modalContainer = true
        },
        CloseModal(modal){
            this.modalContainer = modal
        },
        addData(data){
            console.log('Data...')
            this.data = data
        },
        changeMinutes(value){
            this.count = value
        },
        changeSound(sound){
            this.sound = sound
        }
    }

}

</script>
<style scoped>
h1{
    color: white;
}
button{
    background: none;
    border: none;
}
main{
    display: flex;
    flex-direction: column;
    min-height: 89vh;
    justify-content: space-between;
}
.Home-Header{
    animation: fadeInDown 1s both;
}
  @keyframes fadeInDown {
  0% {
  opacity: 0;
  transform: translate3d(0, -100%, 0);
  }
  100% {
  opacity: 1;
  transform: none;
  }
  } 
</style>