<template>
    <main>
        <h1>pomodoro</h1>
        <HomeNav/>
        <Clock/>
        <wheel/>
    </main>
</template>

<script>
import HomeNav from '../components/HomeNav.vue'
import Clock from '../components/Clock.vue'
import wheel from '../assets/wheel.vue'

export default{
    name: 'Home',
    components: {
        HomeNav,
        Clock,
        wheel
        }
}

</script>
<style scoped>
h1{
    color: white;
}
</style>