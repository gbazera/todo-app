<template>
	<h1>TODO LIST</h1>
	<TodoInput @addItem="addItem"/>
	<h3 v-if="todoItems.length <= 0">Todo list is empty.</h3>
	<TodoItem v-for="(item, index) in todoItems" :key="index" :itemData="item" @removeItem="removeItem" @checkItem="checkItem" @saveItem="updateItem"/>
</template>

<script>
	import TodoInput from './components/todo-input.vue'
	import TodoItem from './components/todo-item.vue'

	export default {
		name: "App",
		components: {
			TodoInput,
			TodoItem,
		},
		data(){
			return {
				todoItems: []
			}
		},
		methods:{
			updateTodoList(){
				for (let i = 0; i < this.todoItems.length; i++) {
					this.todoItems[i].id = i
				}
				localStorage.setItem('todoItems', JSON.stringify(this.todoItems))
			},
			loadTodoList(){
				var newTodoItems = JSON.parse(localStorage.getItem('todoItems'))
				if(newTodoItems){
					this.todoItems = newTodoItems
				}
			},
			addItem(newText){
				var newItem
				newItem = {
					id: this.todoItems.length,
					text: newText,
					checked: false
				}
				this.todoItems.push(newItem)
				this.updateTodoList()
			},
			checkItem(item){
				item.checked = !item.checked
				this.updateTodoList()
			},
			removeItem(i){
				this.todoItems = this.todoItems.filter(todo => todo.id !== i)
				this.updateTodoList()
			},
			updateItem(item, newText){
				item.text = newText
				this.updateTodoList()
			}
		},
		mounted() {
			this.loadTodoList()
		},
	};
</script>

<style>
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif !important;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		width: 600px;
		margin: auto;
		margin-top: 100px;
	}

	*{
		transition: 0.3s;
	}

	button{
		font-size: 18px !important;
	} 

	@media screen and (max-width: 900px){
		#app{
			width: 100%;
		}

		h1{
			font-size: 20px !important;
		}

		h3{
			font-size: 16px !important;
		}

		h4{
			font-size: 12px !important;
		}

		h4 span{
			font-size: 14px !important;
		}
	}
</style>
