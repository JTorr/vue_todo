<template>
  <div class="todoList">
  <div class="sticky" v-for="todo in todos">
    <p class="todoText">
      <i v-if="todo.complete" class="el-icon-circle-check"></i>
      <span v-if="!todo.editing">{{todo.text}}</span>
    </p>
    <input v-on:keyup.enter="saveTodo(todo.id) "v-if="todo.editing" v-model="todo.text" class="todoInput"></input>
    <el-row>
      <el-button-group>
        <el-button type="success" icon="circle-check" size="mini" @click="completeTodo(todo.id)"></el-button>
        <el-button type="info" icon="edit" size="mini" @click="editTodo(todo.id)"></el-button>
        <el-button type="danger" icon="delete" size="mini" @click="removeTodo(todo.id)"></el-button>
      </el-button-group>
    </el-row>
    </div>

    <div class="addTodo">
      <el-button icon="plus" type="success" size="large" @click="addTodo"></el-button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'todo',
  data () {
    return {
      todos: [
             {'id': 0, 'text': 'Make this Vue app', complete: false, editing: false},
             {'id': 1, 'text': 'Use Vue Cli', complete: false, editing: false}
      ],
      newText: '',
      count: 2
    }
  },
  methods: {
    completeTodo (id) {
      let myTodo = this.todos.find((todo) => todo.id === id)
      myTodo.complete = true
    },
    editTodo (id) {
      let myTodo = this.todos.find((todo) => todo.id === id)
      myTodo.editing = true
    },
    saveTodo (id) {
      let myTodo = this.todos.find((todo) => todo.id === id)
      myTodo.editing = false
    },
    removeTodo (id) {
      this.todos = this.todos.filter((todo) => todo.id !== id)
    },
    addTodo () {
      let nextId = this.count++
      this.todos.push({'id': nextId, 'text': '', complete: false, editing: true})
    }
  }
}
</script>

<style scoped>
.sticky {
  height: 100px;
  width: 100px;
  background-color: yellow;
  font-weight: bold;
  margin: 10px;
  box-shadow: 10px 10px 5px #888888;
  display: flex;
  flex-direction: column;
}

.todoText {
  height: 80px;
}

.button-group {
  align: middle;
}

.todoList {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.todoInput {
  height: 500px;
  margin: -10px 5px 10px 5px;
}

.addTodo {
  margin-top: 40px;
  margin-left: 30px;
}
</style>
