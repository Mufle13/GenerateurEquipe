<script>
    export default {
        data: function() {
            return {
                team_number: 2
            }
        }, 
        emits: ["update"],
        methods: {
            increment() {
                this.team_number += this.increment_by
                this.$emit("update", this.team_number)
            },
            decrement() {
                if(this.team_number >= 2) {
                    this.team_number -= 1
                    this.$emit("update", this.team_number)
                } 
            }
        },
        incrementBy() {
            this.count += this.increment_by
        },
        computed: {
            canDecrement() {
                return this.team_number >= 3 ? true : false
            }
        },

        props: {
        increment_by: {
            default: 1
        }
        } 

    }
</script>

<template>
<div class="flex space-x-4 items-center">
<button 
    :class="!canDecrement?'opacity-30 cursor-not-allowed' : 'hover:bg-teal-100'"
    class="rounded-full border-[2px] border-teal-500 w-20 h-20 text-3xl flex justify-center items-center"
    @click="decrement"
    :disabled="!canDecrement">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M5 10a1 1 0 011-1h8a1 1 0 110 2H6a1 1 0 01-1-1z" clip-rule="evenodd" />
        </svg>
</button>
<span class="font-semibold text-xl">{{team_number}}</span>
<button 
    class="rounded-full border-[2px] border-teal-500 w-20 h-20 text-2xl flex justify-center items-center hover:bg-teal-100"  
    @click="increment">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10" viewBox="0 0 20 20" fill="currentColor">
        <path fill-rule="evenodd" d="M10 5a1 1 0 011 1v3h3a1 1 0 110 2h-3v3a1 1 0 11-2 0v-3H6a1 1 0 110-2h3V6a1 1 0 011-1z" clip-rule="evenodd" />
        </svg>
</button>
</div>
</template>