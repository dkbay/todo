<template>
  <div id="app">
    <div class="container">
      <div class="new-todo">
        <input v-on:keyup.enter="addTodo" v-model="newTodo" class="new-todo-input" type="text" placeholder="Dream about potatoes...">
      </div>
      <div class="todos">
        <div v-for="(todo,n) in todos" v-bind:key="todo" class="todo">
          <p class="todo-text">{{ todo }}</p>
          <a class="todo-remove" @click="removeTodo(n)">
            <img src="trash.svg" alt="">
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      todos: [],
      newTodo: "",
    }
  },
  mounted () {
    if (localStorage.getItem('todos')) {
      try {
        this.todos = JSON.parse(localStorage.getItem('todos'))
      } catch(e) {
        localStorage.removeItem('todos')
      }
    }
    // if (localStorage.todoCount) {
    //   this.todoCount = localStorage.todoCount;
    //   for (let i = 0; i < this.todoCount; i++) {
    //     console.log(i);
    //     this.todos.push(localStorage.getItem('todo_'+i));
        
    //   }
    // }
  },
  methods: {
    addTodo() {
      if(!this.newTodo) return;
      this.todos.push(this.newTodo)
      this.newTodo = ''
      this.saveTodos()
    },
    removeTodo(x) {
      this.todos.splice(x,1)
      this.saveTodos();
    },
    saveTodos() {
      let parsed = JSON.stringify(this.todos);
      localStorage.setItem('todos', parsed)
    },
    // persist() {
    //   console.log('Todocount before: '+ this.todoCount)
    //   localStorage.setItem('todo_' + this.todoCount, this.todo);
    //   this.todos.push(this.todo)
    //   this.todoCount = Number(this.todoCount) + 1;
    //   localStorage.setItem('todoCount', this.todoCount)
    //   console.log('Todocount after: '+ this.todoCount)
    // }
  }
}
</script>

<style>
.container {
  display: grid;
  grid-template-columns: 1fr;
  grid-row-gap: 50px;
  justify-items: center;
  justify-content: center;
  width: 80%;
  margin: 50px auto;
}

.new-todo-input {
  padding: 25px;
  font-size: 2em;
  font-weight: bold;
  border: 1px solid #888;
  width:100%;
  border-radius: 3px;
  outline:none;
  background-color: #f3f3f3;
  box-sizing:border-box;
}
.new-todo {
  position: relative;
  max-width:600px;
  width:100%;
  margin-left:-8px;
}

.new-todo::before {
  content: "";
  position: absolute;
  width: 100%;
  height: 100%;
  right: -8px;
  top: 8px;
  background: #21d894;
  border-radius:3px;
  z-index: -1;
}

p, a, input {
  font-family: 'Raleway', sans-serif;
}

.todo {
  display: grid;
  grid-template-columns: 8fr 2fr;
  grid-column-gap: 20px;
  position: relative;
  margin-left:-8px;
  width:100%;
  padding: 25px;
  font-size: 1.2em;
  border: 1px solid #888;
  border-radius: 3px;
  outline:none;
  background-color: #f3f3f3;
  box-sizing: border-box;
  line-height:100%;
}

.todo>a {
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

.todo>a>img {
  height:32px;
}

.todo::before {
  content: "";
  position: absolute;
  width: 100%;
  height: 100%;
  right: -8px;
  top: 8px;
  background: #21d894;
  border-radius:3px;
  z-index: -1;
}

.todos {
  display:grid;
  grid-template-columns: 1fr;
  grid-row-gap: 25px;
  max-width:500px;
  width:100%;
}

.row {
  width:100%;
}
</style>
