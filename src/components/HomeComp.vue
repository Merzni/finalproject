<template>
    <div class="template">
        <div v-if="isAuthenticated">
            <div>Добро пожаловать <b>{{ username }}</b></div>
            <button @click="logout" class="login">Выйти с аккаунта</button>
        </div>

        <div v-else>
            <label>Ваше имя : </label>
            <input v-model="username" @keyup.enter="login"/>
            <button @click="login" class="login">Войти</button>
        </div>

    </div>
</template>

<script>
export default{
    name: 'HomePage',
    data(){
        return{
            isAuthenticated: false,
            username: ''
        }
    },

    methods: {
        login(){
            if(this.username !== ''){
                console.log('Вы вошли в свой аккаунт')
                this.isAuthenticated = true
                localStorage.setItem('isAuthenticated', true)
                localStorage.setItem('username', this.username)
                this.$router.push({
                    name: 'Chat',
                    query: {username: this.username}
                })
            }else{
                console.log('Пожалуйста, введите свое имя!')
            }
        },
        logout(){
            this.isAuthenticated = false
            this.username = ''
            localStorage.removeItem('isAuthenticated')
            localStorage.removeItem('username')
        }
    },

    created(){
        if(localStorage.getItem('isAuthenticated')){
            this.isAuthenticated = true
            this.username = localStorage.getItem('username')
        }
    }
}
</script>

<style scoped>

div{
    padding: 20px;
    font-size: 25px;
}

input{
    width: 125px;
    height: 20px;
    border-radius: 8px;
    border: 1px solid black;

    font-family: 'Helvetica';
}

label{
    margin: 1px;
}

button{
    margin-left: 10px;
}

.login{
    width: auto;
    height: 30px;
    border: 2px solid rgb(255, 255, 255);
    border-radius: 4px;
    background-color: rgba(255, 255, 255, 0);
    color: white;

    font-family: 'Helvetica';
    font-size: 16px;

    transition: 0.5s;
}

.login:hover{
    color: black;
    background-color: white;
}

.login:active{
    background-color: rgb(197, 197, 197);
    border: 2px solid rgb(197, 197, 197);
}
</style>