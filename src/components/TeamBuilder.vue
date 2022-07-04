<script>
export default {
    data: function () {
        return {
            members: [],
            team_number: 2,
            final_teams: [],
            display_result: false
        };
    },
    methods: {
        addMember(name) {
            if(this.members.includes(name)) {
                alert("Il y a dejà un nom similaire dans la liste")
                return
            }
            this.members.push(name);
        },

        updateTeamNumber(team_number) {
            this.team_number = team_number
        },
        removeMember(member) {
            let member_index = this.members.indexOf(member)
            this.members.splice(member_index, 1)
        },
        generateTeams() {
            if(this.members.length == 0) {
                return
            }

            let final_teams = []
            let shuffled_members = [...this.members].sort(() => 0.5 - Math.random())
            for (let i = 0; i < this.team_number; i++) {
                 final_teams.push([])
            }
            
            let j = 0
            while (j < shuffled_members.length) {
                for (let i = 0; i < this.team_number; i++) {
                    final_teams[i].push(shuffled_members[j])
                    j++
                }
            }
            this.final_teams = final_teams
            this.display_result = true


        },
        reshuffleTeams() {
        }
    },
    computed: {
        is_valid() {
            if(this.members.length == 0) {
                return false
            }
            else if(this.members.length < this.team_number) {
                return false
            }
            return true
        }
    },
    components: { NameInput, TeamsCounter, TeamResult }
}
import NameInput from './NameInput.vue'
import TeamsCounter from './TeamsCounter.vue';
import TeamResult from './TeamResult.vue';
</script>

<template>
<div class="h-full flex flex-col justify-center">
    <div class="xl:h-64 h-full flex justify-center bg-gradient-to-r from-cyan-500 to-teal-500">
        <h1 class="m-16 m-15 text-4xl font-semibold text-white">Générateur d'équipe</h1>
    </div>
    <div class="bg-white rounded-md xl:shadow-md flex justify-center items-center xl:w-[600px] xl:min-h-[400px] h-auto w-full relative m-auto bottom-36">
        <transition name="rotate">
        <div v-if="!display_result" class="flex flex-col items-start space-y-3 p-10 rounded-md w-full h-full">
            
            <NameInput @addName="addMember"></NameInput>
            <div class="text-2xl">Listes des joueurs ({{members.length}}):</div>
            <div class="flex flex-wrap xl:min-h-[50px] min-h-[2em]">
                <transition-group name="fade">
                    <span 
                        v-for="member in members"
                        :key="member"
                        class="border border-gray-400 rounded-md px-3 py-2 flex items-center space-x-3 mr-2 mb-2">
                        <span>{{member}}</span> 
                        <button @click="removeMember(member)">
                            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-red-500" viewBox="0 0 20 20" fill="currentColor">
                                <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd" />
                            </svg>
                        </button>
                    </span>
                </transition-group>
            </div>
            <div>
                <div class="text-2xl mb-8">Nombre d'équipe souhaité : </div>
                <TeamsCounter @update="updateTeamNumber"/>
            </div>
            <div class="flex w-full justify-end">
                <button v-on="is_valid ? {click: generateTeams} : {}" :disabled="!is_valid" class="btn" :class="!is_valid ? 'opacity-30 cursor-not-allowed': ''">
                C'est tipar</button>
            </div>
        </div>
        <div v-else class="bg-white xl:shadow-md flex flex-col items-start space-y-3 p-10 rounded-md absolute top-0 left-0 w-full min-h-[400px] h-auto">
            <div class="flex flex-col w-full min-h-[300px] h-auto">
                <TeamResult :final_teams="final_teams"></TeamResult>
            </div>
            <div class="flex justify-end w-full">
                <button @click="display_result=false" class="btn">Back</button>
            </div>
        </div>
        </transition>
    </div>
</div>

</template>

<style>
.fade-enter-active,
.fade-leave-active {
    transition: all 0.5s ease;
} 

.fade-enter-from
{
    opacity: 0;
    transform: translateY(-15px);
}

.fade-leave-to {
    opacity: 0;
    transform: translateY(15px);
}
.rotate-leave-active,
.rotate-enter-active {
    transition: all 1s ease;
}




.rotate-enter-from
{
    opacity: 0;
    transform: rotateY(180deg);
}

.rotate-leave-to {
    opacity: 0;
    transform: rotateY(180deg);
}

</style>