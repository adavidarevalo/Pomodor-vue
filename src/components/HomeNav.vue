<template>
    <header>
        <nav>
            <button 
            @click="selectButton(dataContainer.pomodoro, 1)" 
            v-bind:style="{background: Count === 1 ? colorButton : none}"
            v-bind:class="{ active: Count === 1 }"
            >pomodoro</button>
            <button 
            @click="selectButton(dataContainer.shortbreak, 2)" 
            v-bind:style="{background: Count === 2 ? colorButton : none}"
            v-bind:class="{ active: Count === 2 }"
            >short break</button>
            <button 
            @click="selectButton(dataContainer.longbreak, 3)" 
            v-bind:style="{background: Count === 3 ? colorButton : none}"
            v-bind:class="{ active: Count === 3 }"
            >long break</button>
        </nav>
    </header>
</template>
<script>
let  audioSlide = new Audio(require('../assets/sounds/slide.mp3'))

export default {
    name: 'HomeNav',
    props: ['data'],
    data(){
        return{
            Count: 1,
            colorButton: '#F87070',
            dataContainer: {
                pomodoro: 25,
                shortbreak: 5,
                longbreak: 15,
                font: 'Arial',
                color: '#F87070'
            }
        }
    },
    watch: {
        data: function (data) {
            console.log('si ',data)
            this.dataContainer = data
            this.colorButton = data.color
            console.log('this.dataContainer ',this.dataContainer)
        }
    },
    methods: {
        selectButton(value, number){
            audioSlide.play()
            this.$emit('count', value)
            this.Count = number
        }
    }
}

</script>

<style scoped>
nav{
    width: 95%;
    background: #171932;
    margin: 0 auto;
    border-radius: 1000px;
    display: flex;
    justify-content: space-between;
    padding: 5px;
    max-width: 350px;
}
button{
    border-radius: 100px;
    border: none;
    padding: 10px 6px;
    font-size: 1rem;
    color: #d7e0ffcc;
    background: none;
    font-weight: 700;
    cursor: pointer;
}
.active{
    color: #1e213f;
}
</style>