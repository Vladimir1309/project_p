<template>
    <div class="home">
        <div v-if="isAuthenticated" class="home_h">
            <br><div>Приветствую вас, уважаемый (-ая) <b>{{ username }}</b></div><br>
            <button @click="logout">Выйти</button>
        </div>

        <div v-else class="home_h">
            <br><label>Введите имя: </label><br><br>
            <input v-model="username"/>
            <button @click="login">Сохранить</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'HomePage',
    data(){
        return {
            isAuthenticated: false,
            username: ''
        }
    },
    methods: {
        login(){
            if(this.username !== ''){
                this.isAuthenticated = true
                localStorage.setItem('isAuthenticated', true)
                localStorage.setItem('username', this.username)

                this.$router.push({
                    name: 'Chat',
                    query: {username: this.username}
                })
            } else {
                alert('Напишите имя')
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
        if(localStorage.getItem('isAuthenticated')) {
            this.isAuthenticated = true
            this.username = localStorage.getItem('username')
        }
    }
}
</script>

<style>
.home {
    margin-top: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 70%;
}

.home_h {
    border: 5px solid darkkhaki;
    border-radius: 10px;
    padding: 20px;
    background-color: bisque;
    color: black;
}
</style>