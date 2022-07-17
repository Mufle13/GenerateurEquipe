<script>
export default {
    data: function() {
        return {
            is_flipped: false,
            team_names_dico: {},
            teams_names_list: [],
            edit: {}
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
        updateEdit(index) {
            this.edit[index] = !this.edit[index]
        }
    },
    created: function() {
        for (let i = 0; i < this.final_teams.length; i++) {
            this.team_names_dico[i] = `Equipe ${i + 1}`
            this.edit[i] = false
        }
    },

    props: ["final_teams"],

}
</script>

<template>
<div class="flex items-start justify-between w-full h-full flex-wrap">
    <div v-for="(team, index) in final_teams" class="py-5 px-5 mb-3 border border-teal-500 rounded-md flex flex-col items-center bg-white drop-shadow-lg">
        <div class="flex flex-col space-y-5" v-if="edit[index] == true"> 
            <div class="flex">
                <input 
                placeholder="Entrer le nom de l'équipe" 
                type="text"
                v-model="team_names_dico[index]"
                @keyup.enter="addTeamName(index)" 
                autocomplete="off"
                class="w-3/4 p-2 rounded-md text-sm">
                <button @click="updateEdit(index)">
                    <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                        <path d="M13.586 3.586a2 2 0 112.828 2.828l-.793.793-2.828-2.828.793-.793zM11.379 5.793L3 14.172V17h2.828l8.38-8.379-2.83-2.828z" />
                    </svg>
                </button>
            </div>
            <span v-for="player in team">{{player}}</span>
        </div>      
        <div class="flex flex-col space-y-5" v-else>
            <div class="mb-5 font-semibold text-lg">{{team_names_dico[index]}}
            <button @click="updateEdit(index)">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
                    <path d="M13.586 3.586a2 2 0 112.828 2.828l-.793.793-2.828-2.828.793-.793zM11.379 5.793L3 14.172V17h2.828l8.38-8.379-2.83-2.828z" />
                </svg>
            </button>
            </div>  
            <span v-for="player in team">{{player}}</span>
        </div>
    </div>
</div>
</template>