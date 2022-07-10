<script>
export default {
    data: function() {
        return {
            is_flipped: false,
            team_name: "",
            teams_names: []
        }
    },
    methods: {
        addTeamName() {
            this.team_name = this.team_name.trim()
            if(this.team_name.trim() != "") {
                this.team_name = this.team_name.charAt(0).toUpperCase() + this.team_name.slice(1)
                if(this.teams_names.includes(this.team_name)) {
                alert("Ce nom d'équipe est déja pris !")
                return
            }
                this.teams_names.push(this.team_name)
                this.team_name = ""
        }
    },
    },
    props: ["final_teams"]

}
</script>

<template>
<div class="flex items-start justify-between w-full h-full flex-wrap">
    <div v-for="(team, index) in final_teams" class="py-5 px-5 mb-3 border border-teal-500 rounded-md flex flex-col items-center bg-white drop-shadow-lg">
        <div class="flex flex-col space-y-5" v-if="teams_names[index] == undefined">
            <div class="mb-5 font-semibold text-lg">Equipe {{ index + 1}}</div>  
                <input 
                placeholder="Entrer le nom de l'équipe" 
                type="text"
                v-model="team_name"
                @keyup.enter="addTeamName" 
                autocomplete="off"
                class="w-3/4 p-2 rounded-md text-sm">
                <span v-for="player in team">{{player}}</span>
        </div>
        <div class="flex flex-col space-y-5" v-else>
            <div class="mb-5 font-semibold text-lg">{{teams_names[index]}}</div>  
            <span v-for="player in team">{{player}}</span>
        </div>
    </div>
</div>
</template>