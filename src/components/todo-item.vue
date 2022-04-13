<template>
    <div class="todo-item" v-bind:class="{'todo-item-checked': itemData.checked}">
        <div class="left">
            <span>{{ itemData.id + 1 }}</span>
            <input type="text" v-model="inputText" ref="input">
        </div>
        <div class="right">
            <button class="edit btn btn-primary btn-sqr" v-bind:class="{'edit-active': canEdit}" v-on:click="editItem"><i class='bx bx-edit-alt'></i></button>
            <button class="check btn btn-success btn-sqr" v-on:click="checkItem"><i class='bx bx-check'></i></button>
            <button class="remove btn btn-danger btn-sqr" v-on:click="removeItem"><i class='bx bx-x'></i></button>
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
    data() {
        return {
            inputText: this.itemData.text,
			canEdit: false
        }
    },
	mounted() {
		this.$refs.input.disabled = true
		this.$refs.input.blur()
	},
    methods: {
        saveItem : function(){
            this.$emit('saveItem', this.itemData, this.inputText)
        },
        editItem : function(){
            if(this.itemData.checked) return

			if(this.canEdit){
				this.canEdit = false
				this.$refs.input.disabled = true
				this.$refs.input.blur()
				this.saveItem()
			}else{
				this.canEdit = true
				this.$refs.input.disabled = false
				this.$refs.input.focus()
			}
        },
        checkItem : function(){
            if(this.canEdit) return
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
        border-bottom: 2px #2c3e5020 solid;
        padding: 10px;
    }

    .todo-item:last-of-type{
        border: none;
    }

    .todo-item-checked{
        opacity: 0.5;
        text-decoration: line-through;
    }

    input{
        font-size: 18px;
        color: #2c3e50;
        border: none;
		outline: none;
        margin-left: 5px;
    }

    input:focus{
        border-bottom: 1px #2c3e50 solid;
    }

    button{
        margin: 0;
        margin-left: 5px;
    }

    /* button{
        border: none;
        cursor: pointer;
        width: 40px;
        height: 40px;
        border-radius: 5px;
        margin-left: 5px;
    }

    .edit{
        background-color: lightsteelblue;
        color: darkslategray;
    }

	.edit-active{
		background-color: slategray;
		color: whitesmoke;
	}

    .check{
        background-color: lightgreen;
        color: darkgreen;
    }

    .remove{
        background-color: lightcoral;
        color: darkred;
    } */

    span{
        font-size: 32px;
    }
</style>