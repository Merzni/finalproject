<template>
    <div class="container">
        <nav>
            <router-link to="/" class="router-link">Домашняя страница</router-link>
            <router-link to="/chat" class="router-link">Чат</router-link>
            <router-link to="/test" class="router-link">Тест API</router-link>
        </nav>
    </div>
</template>

<script>
export default {
    name: 'NavComp'
}
</script>

<style>
.container {
    background-color: greenyellow;
    height: 60px;
    display: flex;
    justify-content: center;
}

nav{
    width: 400px;
    height: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px;
}

.router-link{
    color: rgb(255, 255, 255);
    text-decoration: none;
}

.router-link:hover{
    color: rgb(224, 224, 224);
}
</style>