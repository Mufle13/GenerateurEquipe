<script>
export default {
    data: function() {
        return {
            is_flipped: false
        }
    },
    methods: {},
    props: ["final_teams"]

}
</script>

<template>
<div class="flex items-start justify-between w-full h-full flex-wrap">
    <div v-for="(team, index) in final_teams" class="py-5 px-5 mb-3 border border-teal-500 rounded-md flex flex-col items-center bg-white drop-shadow-lg">
        <div class="mb-5 font-semibold text-lg">Equipe {{index + 1}}</div>  
            <span v-for="player in team">{{player}}</span>
    </div>
</div>
</template>