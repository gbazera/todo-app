<template>
    <form class="todo-input" onsubmit="return false">
        <input type="text" v-model="inputText" autofocus>
        <button type="submit" v-on:click="addItem"><i class='bx bx-plus'></i></button>
    </form>
</template>

<script>
export default{
    data() {
        return {
            inputText: '',
        }
    },
    props:{
        
    },
    methods: {
        addItem(){
            if (this.inputText === ''){
                return
            }
            this.$emit('addItem', this.inputText)
            this.inputText = ''
        }
    },
}
</script>

<style scoped>
    .todo-input{
        display: flex;
        height: 40px;
        margin-bottom: 10px;
    }

    input, button{
        border: none;
    }

    input{
        background-color: gainsboro;
        width: 100%;
        border-radius: 5px 0px 0px 5px;
        padding: 10px;
        font-size: 18px;
        color: #2c3e50;
        outline: none;
    }

    button{
        width: 40px;
        border-radius: 0px 5px 5px 0px;
        background-color: lightgreen;
        color: darkgreen;
        cursor: pointer;
    }
</style>