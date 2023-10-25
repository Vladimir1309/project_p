<template>
    <div class="team">

        <div class="title_teams">Команды</div>
        <div>
            <div v-if="isLoad">Загрузка данных...</div>
            <div v-else>
                <div class="player" v-for="el in teamData" :key="el.id">
                    {{ el.id }}. {{ el.abbreviation }} {{ el.city }}
                    <img src="https://cdn-icons-png.flaticon.com/512/1345/1345823.png" style="width: 15px; height: 15px"
                        @click="removeTeam(el.id)" />
                </div>

            </div>
        </div>


    </div>
</template>

<script>
export default {
    name: 'TestApi',
    data() {
        return {
            teamData: [],
            isLoad: true
        }
    },
    mounted() {
        const url = 'https://free-nba.p.rapidapi.com/teams?page=0';
        const options = {
            method: 'GET',
            headers: {
                'X-RapidAPI-Key': 'f41206f6cemsh627a230ed06078ep100f32jsn8b01f0c821e3',
                'X-RapidAPI-Host': 'free-nba.p.rapidapi.com'
            }
        };

        fetch(url, options)
            .then((res) => res.json())
            .then((res) => {
                console.log(res);
                this.teamData = res.data
                this.isLoad = false
            })

    },
    methods: {
        removeTeam(id) {
            this.teamData = this.teamData.filter((el) => el.id !== id)
        }
    }
}
</script>

<style>
.team {
    margin-top: 1px;
    line-height: 1.45;
}

.player {
    border: 2.5px solid darkkhaki;
    line-height: 23px;
    border-radius: 5px;
    background-color: bisque;
    color: black
}

.title_teams {
    border: 3px solid black;
    border-radius: 10px;
    padding: 5px;
    background-color: bisque;
    color: black;
    margin-top: 15px;
    margin-bottom: 15px;
}
</style>