<template>
    <div class="nav">
        <nav>
            <div class="nav_1"><router-link to="/">Главная</router-link></div>
            <div class="nav_1"><router-link to="/chat">Чат</router-link></div>
            <div class="nav_1"><router-link to="/test">NBA</router-link></div>
        </nav>
    </div>
</template>

<script>
export default {
    name: 'NavComponent',
}
</script>

<style scoped>
.nav {
    background-color: darkseagreen;
    width: 100%;
    display: flex;
    justify-content: center;
    height: 70px;
}

nav {
    width: 500px;
    height: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.nav_1 {
    border: 3px solid black;
    border-radius: 10px;
    padding: 10px;
    background-color: aqua;
}
</style>
