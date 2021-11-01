<template>
    <main>
        <div>
            <h1>pomodoro</h1>
            <HomeNav :data='data'/>
        </div>
        <Clock/>
        <button @click="OpenModal()">
            <wheel/>
        </button>
        <Modal 
        :modalContainer='modalContainer' 
        @close='CloseModal($event)' 
        @data='addData($event)'/>
    </main>
</template>

<script>
import HomeNav from '../components/HomeNav.vue'
import Clock from '../components/Clock.vue'
import wheel from '../assets/wheel.vue'
import Modal from '../components/Modal.vue'

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
            }
        }
    },
    methods:{
        OpenModal(){
            this.modalContainer = true
        },
        CloseModal(modal){
            this.modalContainer = modal
        },
        addData(data){
            this.data = data
            console.log('this.data ', this.data)
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
</style>