<script>
export default {
    data: function() {
        return {
            name: ""
        }
    },
    emits: ["addName"],
    methods: {
        submitName() {
            this.name = this.name.trim()
            if(this.name.trim() != "") {
                this.name = this.name.charAt(0).toUpperCase() + this.name.slice(1)
                this.$emit("addName", this.name)
                this.name = ""
            }
            
        }
    }
}
</script>

<template>
<input 
    placeholder="Entrer le nom d'un joueur" 
    id="name" type="text" 
    v-model="name"
    @keyup.enter="submitName" 
     autocomplete="off"
    class="w-3/4 p-2 rounded-md text-xl">
</template>

<style>
input {
    border: solid 1px grey;
    padding: 5px;
}

button {
    padding: 5px;
    margin-left: 10px;
}

</style>