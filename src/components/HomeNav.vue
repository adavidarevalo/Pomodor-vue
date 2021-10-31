<template>
    <header>
        <nav>
            <button 
            @click="selectButton(25)" 
            v-bind:style="{background: Count === 25 ? colorButton : none}"
            v-bind:class="{ active: Count === 25 }"
            >pomodoro</button>
            <button 
            @click="selectButton(3)" 
            v-bind:style="{background: Count === 3 ? colorButton : none}"
            v-bind:class="{ active: Count === 3 }"
            >short break</button>
            <button 
            @click="selectButton(15)" 
            v-bind:style="{background: Count === 15 ? colorButton : none}"
            v-bind:class="{ active: Count === 15 }"
            >long break</button>
        </nav>
    </header>
</template>
<script>

export default {
    name: 'HomeNav',
    data(){
        return{
            Count: 25,
            colorButton: '#F87070'
        }
    },
    methods: {
        selectButton(value){
            this.Count = value
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
}
button{
    border-radius: 100px;
    border: none;
    padding: 10px 6px;
    font-size: 1rem;
    color: #d7e0ffcc;
    background: none;
    font-weight: 700;
}
.active{
    color: #1e213f;
}
</style>