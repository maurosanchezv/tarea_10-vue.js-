<template>
  <div>
    <h1>lista de tareas</h1>
    <!-- formulario de entrada de tareas -->
    <form @submit.prevent="addTodo()">
      <el-input placeholder="todo" v-model="todo"></el-input>
    </form>
    <el-row :gutter="12">
      <!-- área de visualización de tareas pendientes -->
      <TodoItem 
        v-for="(todo, index) in todos" 
        :key="index" 
        :item="todo" 
        :index="index"
        type="todo"
        @remove-todo="removeTodo"
      />
    </el-row>
    
    <h1>lista de problemas</h1>
    <el-button type="success" @click="getIssues">Obtener emisión</el-button>
    <el-row :gutter="12">
      <!-- zona de visualización de problemas -->
      <TodoItem 
        v-for="(issue, index) in issues" 
        :key="issue.id" 
        :item="issue" 
        :index="index"
        type="issue"
        @close-issue="closeIssue"
      />
    </el-row>
  </div>
</template>
  
  <script>
  import axios from 'axios';
  import TodoItem from '@/components/TodoItem';
  
  const client = axios.create({
    baseURL: `${process.env.VUE_APP_GITHUB_ENDPOINT}`,
    headers: {
      'Authorization': `token ${process.env.VUE_APP_GITHUB_TOKEN}`,
      'Accept': 'application/vnd.github.v3+json',
      'Content-Type':'application/json',
    },
  })
  
  export default {
  name: 'TodosIssues',
  components: {
    TodoItem
  },
  data () {
    return {
      todo: '',
      todos: [],
      issues: []
    }
  },
  methods: {
    addTodo(){
      this.todos.push(this.todo);
      this.todo= '';
    },
    removeTodo(index){
      this.todos.splice(index, 1);
    },
    closeIssue(index){
      const target = this.issues[index];
      client.patch(`/issues/${target.number}`,
          {
            state: 'closed'
          },
        )
        .then(() => {
         this.issues.splice(index, 1);
      })
    },
    getIssues() {
      client.get('issues')
        .then((res) => {
          this.issues = res.data
      })
    }
  },
  created() {
    this.getIssues();
  }
}
</script>