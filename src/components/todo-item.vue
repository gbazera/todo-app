<template>
    <div class="todo-item" v-bind:class="{'todo-item-checked': itemData.checked}">
        <h4><span>{{ itemData.id + 1 }}</span> {{ itemData.text }}</h4>
        <div class="buttons">
            <button class="check" v-on:click="checkItem"><i class='bx bx-check'></i></button>
            <button class="remove" v-on:click="removeItem"><i class='bx bx-x'></i></button>
        </div>
    </div>
</template>

<script>
export default{
    props:{
        itemData:{
            type: Object,
            required: true,
        }
    },
    methods: {
        checkItem : function(){
            this.$emit('checkItem', this.itemData)
        },
        removeItem : function(){
            this.$emit('removeItem', this.itemData.id)
        }
    },
}
</script>

<style scoped>
    .todo-item {
        margin: auto;
        display: flex;
        align-items: center;
        justify-content: space-between;
        border-bottom: 2px #2c3e50 solid;
    }

    .todo-item:last-of-type{
        border: none;
    }

    .todo-item-checked{
        opacity: 0.5;
        text-decoration: line-through;
    }

    button{
        border: none;
        cursor: pointer;
        width: 40px;
        height: 40px;
        border-radius: 5px;
        margin-left: 5px;
    }

    .check{
        background-color: lightgreen;
        color: darkgreen;
    }

    .remove{
        background-color: lightcoral;
        color: darkred;
    }

    span{
        font-size: 32px;
    }
</style>