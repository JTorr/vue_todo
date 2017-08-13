<template>
  <div class="todoList">
  <div class="sticky" v-for="todo in todos">
    <span class="todoText">{{todo.text}}</span>
    <i v-if="todo.complete" class="el-icon-check"></i>
    <el-row>
      <el-button-group>
        <el-button type="success" icon="circle-check" size="mini" @click="completeTodo(todo.id)"></el-button>
        <el-button type="info" icon="edit" size="mini"></el-button>
        <el-button type="danger" icon="delete" size="mini" @click="removeTodo(todo.id)"></el-button>
      </el-button-group>
    </el-row>
    </div>
  </div>
</template>

<script>
export default {
  name: 'todo',
  data () {
    return {
      todos: [
             {'id': 1, 'text': 'Make this Vue app', 'complete': false},
             {'id': 2, 'text': 'Use Vue Cli', 'complete': false}
      ]
    }
  },
  methods: {
    completeTodo (id) {
      let myTodo = this.todos.find((todo) => todo.id === id)
      myTodo.complete = true
    },
    editTodo (id, newText) {
      let myTodo = this.todos.find((todo) => todo.id === id)
      myTodo.text = newText
    },
    removeTodo (id) {
      this.todos = this.todos.filter((todo) => todo.id !== id)
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
</style>
