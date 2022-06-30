<script>
export default {
    props: {
        increment_by: {
            default: 1
        }, 
        background_color:
        {
            default: "skyblue"
        }
    },
    data: function() {
        return {
            count: 0
        }
    },
    methods: {
        incrementBy() {
            this.count += this.increment_by
        },

    }

}


</script>

<template>
<div @click="increment" :style="'background-color:' + background_color">Counter: {{count}}</div>
</template>

<style scoped>
div {
border-radius: 20px;
border: solid 1px pink;
background-color: skyblue;
width: 20%;
cursor: pointer
}
</style>