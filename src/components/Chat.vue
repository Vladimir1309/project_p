<template>
    <div v-if="username">
        <div class="chat">
            <h2>Чат</h2><br>
            <div class="text" v-for="message in messages" :key="message.id">
                {{ message.user }}: {{ message.text }}
            </div>

            <div v-show="emptyMsg" class="empty">Текущих сообщений нет</div>
        </div>

        <input v-model="newMessage" placeholder="Введите сообщение"/>
        <button @click="sendMessage">Отправить</button>
        <button @click="delMessage">Удалить</button>
    </div>

    <div v-else>
        Для авторизации перейдите по <router-link :to='{name: "Home"}'>ссылке</router-link>
    </div>
</template>



<script>
export default {
    name: 'ChatComp',
    data(){
        return {
            messages: [],
            newMessage: '',
            emptyMsg: true,
            username: localStorage.getItem('username')
        }
    },
    computed(){
        localStorage.setItem('username', this.$route.query.username)
    },
    methods: {

        sendMessage(){
            if(this.newMessage !== '') {
                this.emptyMsg = false
                this.messages.push({id: new Date().getTime(), text: this.newMessage, user: this.username})
                this.saveChatRecords()
                this.newMessage = ''
            } else {
                alert ('Введите сообщение')
            }
        },
        saveChatRecords(){
            const records = this.messages
            localStorage.setItem(`messages_${this.message}`, JSON.stringify(records))
        },
        loadChatRecords(){
            const records = JSON.parse(localStorage.getItem(`messages_${this.message}`))
            if(records){
                this.messages = records
                this.emptyMsg = false
            }
        },
        delMessage(){
            this.messages = []
            localStorage.removeItem(`messages_${this.message}`, JSON.stringify(this.messages))
            this.emptyMsg = true
        }
    },
    created(){
        this.loadChatRecords()
    }
}


</script>

<style>


h2 {
    color: orchid
}

.text {
    margin-bottom: 20px;
}

.chat {
    width: 400px;
    height:83%;
    border: 5px solid darkkhaki;
    background-color: blanchedalmond;
    color: black;
    font-weight: 18px;
    font-weight: bold;
    margin: 20px;
    padding: 15px;
    border-radius: 10px;
}

input {
    margin-right: 10px;
    background-color:blanchedalmond;
}

button {
    margin-left: 5px;
    margin-bottom: 25px;
    background-color:blanchedalmond;
}

.alert {
    padding: 30px;
}

.empty {
    margin-bottom: 25px;
    font-style: italic;
}
</style>