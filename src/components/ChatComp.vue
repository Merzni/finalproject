<template>
    <div v-if="username">
        <div class="chat">
            <h2>Чат</h2>
            <div class="text" v-for="message in messages" :key="message.id">
            {{ message.user }} : {{ message.text }}</div>
        </div>
        <div v-show="emptyMsg" class="empty">
            Нету сообщений
        </div>
        <input v-model="newMessage" placeholder="Сообщение">
        <button @click="sendMessage" @keyup.enter="sendMessage">Отправить</button>
        <button v-show="deleteBtn" @click="delMessage">Удалить</button>
    </div>
    <div v-else class="alert">
        Для того чтобы использовать чат, перейдите в <router-link :to="{ name: 'Home' }">на главную страницу</router-link>
    </div>
</template>

<script>
export default {
    name: 'ChatPage',
    data(){
        return{
            messages: [],
            newMessage: '',
            emptyMsg: true,
            deleteBtn: false,
            username: localStorage.getItem('username')
        }
    },
    computed(){
        localStorage.setItem('username', this.$route.query.username)
    },
    methods: {
        sendMessage(){
            if(!this.username){
                this.username = "Anonim"
            }
            if(this.newMessage !== ''){
                this.emptyMsg = false
                console.log('Вы отправили сообщение:', this.newMessage)
                this.messages.push(
                    {
                        id: new Date().getTime,
                        text: this.newMessage,
                        user: this.username
                    }
                )
                this.saveChatRecords()
                this.newMessage = ''
                this.deleteBtn = true
            }else{
                console.log('Введите сообщение')
                alert('Введите сообщение')
            }
        },
        delMessage(){
            this.messages = []
            localStorage.removeItem(`messages_${this.username}`, JSON.stringify(this.message))
            console.log("Все сообщения удалены")
            this.emptyMsg = true
        },
        saveChatRecords(){
            const records = this.messages
            console.log(records)
            localStorage.setItem(`messages_${this.username}`, JSON.stringify(records))
        },
        loadChatRecords(){
            const records = JSON.parse(localStorage.getItem(`messages_${this.username}`))
            if(records){
                this.messages = records
                this.emptyMsg = false
            }
        }
    },
    created(){
        this.loadChatRecords()
    }
}
</script>

<style>
    h2{
        color: rgb(255, 255, 255);
        text-decoration: underline;
    }

    .text{
        margin-bottom: 25px;
    }

    .chat{
        width: 600px;
        height: 100%;
        border: 4px solid rgb(255, 255, 255);
        border-radius: 16px;
        background-color: rgba(255, 255, 255, 0);
        color: rgb(255, 255, 255);
        font-weight: 20px;
        margin: 20px;
        padding: 15px;
    }

    .empty{
        margin-bottom: 30px;
        font-style: italic;
    }

    input{
    width: 125px;
    height: 20px;
    border-radius: 8px;
    border: 1px solid black;

    font-family: 'Helvetica';
    margin-right: 10px;
    margin-bottom: 10px;
    }

    button{
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

    button:hover{
        color: black;
        background-color: white;
    }

    button:active{
        background-color: rgb(197, 197, 197);
        border: 2px solid rgb(197, 197, 197);
    }

    .alert{
        padding: 30px;
    }
</style>