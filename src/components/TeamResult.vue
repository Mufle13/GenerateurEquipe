<script>
export default {
    data: function() {
        return {
            is_flipped: false,
            team_names_dico: {},
            teams_names_list: []
        }
    },
    methods: {
        addTeamName(index) {
            let name = this.team_names_dico[index]
            name = name.trim()
            console.log(name)
            if(name != "") {
                name = name.charAt(0).toUpperCase() + name.slice(1)
                if(this.teams_names_list.includes(name)) {
                alert("Ce nom d'équipe est déja pris !")
                return
            }
                this.teams_names_list.push(name)
        }
    },
    },
    created: function() {
        for (let i = 0; i < this.final_teams.length; i++) {
            this.team_names_dico[i] = "Equipe ${i}"
        }
    },

    props: ["final_teams"]

}
</script>

<template>
<div class="flex items-start justify-between w-full h-full flex-wrap">
    <div v-for="(team, index) in final_teams" class="py-5 px-5 mb-3 border border-teal-500 rounded-md flex flex-col items-center bg-white drop-shadow-lg">
        <div class="flex flex-col space-y-5" v-if="teams_names_list[index] == undefined">
            <div class="mb-5 font-semibold text-lg">Equipe {{ index + 1}}</div>  
                <input 
                placeholder="Entrer le nom de l'équipe" 
                type="text"
                v-model="team_names_dico[index]"
                @keyup.enter="addTeamName(index)" 
                autocomplete="off"
                class="w-3/4 p-2 rounded-md text-sm">
                <span v-for="player in team">{{player}}</span>
        </div>
        <div class="flex flex-col space-y-5" v-else>
            <div class="mb-5 font-semibold text-lg">{{teams_names_list[index]}}</div>  
            <span v-for="player in team">{{player}}</span>
        </div>
    </div>
</div>
</template>