<template>
  <main>
    <v-subheader>List of Todos</v-subheader>
    <v-text-field
    :append-icon="'mdi-plus'"
    class="pa-4"
    outlined
    @keyup.enter="addTodo"
    name="addBtn"
    label="Add Todo"
    hide-details
    clearable
    v-model="newTodo.name"
    @click:append="addTodo"
  ></v-text-field>
  <div
  v-for="task in tasks"
  :key="task.id"
  >
    <v-list-item>
      <template v-slot:default>
        <v-list-item-action>
          <v-checkbox :input-value="task.done" color="#7B1FA2"></v-checkbox>
        </v-list-item-action>

        <v-list-item-content @click="doneTask(task.id)" :class="{ 'text-decoration-line-through': task.done}" class="pa-4 rounded"> 
          <v-list-item-title>{{task.name}}</v-list-item-title>
        </v-list-item-content>
        <v-list-item-action>
          <button @click="deleteTask(task.id)">
          <v-icon color="red">mdi-delete</v-icon></button>
        </v-list-item-action>
      </template>
    </v-list-item>
    <v-divider></v-divider>
</div>
</main>
</template>

<script>
export default{
  name: 'HomeComp',
  data(){
    return {
      tasks : [
        {id: 1, name: 'Wake up', done: false},
        {id: 2, name: 'Brush Teeth', done: false},
        {id: 3, name: 'Tell yourself React is the best UI library', done: false},
      ],
      newTodo: {id: "", name: "", done: false},
    }
  }, 
  methods: {
    doneTask(id){
      let task = this.tasks.filter((task) => task.id === id)[0]
      task.done = !task.done
    },
    deleteTask(id){
      this.tasks =  this.tasks.filter(task => task.id !== id)
    },
    addTodo(){
      if(this.newTodo !== ""){
        this.tasks.push(this.newTodo)
        this.newTodo.id = this.tasks.length + 1
      }
      this.newTodo = {}
    }
  }
}
</script>