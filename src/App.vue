<script>
import NavComp from './components/NavComp.vue';

export default {
    name: 'App',
    components: {
        NavComp
    }
}
</script>

<template>
    <div class="container"> 
        <NavComp/>
        <router-view></router-view>
    </div>
</template>

<style scoped>
.container{
    background-color: rgba(255, 255, 255, 0.096);
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 100%;

    color: white;
}
</style>
