<template>
  <div id="app">
    <div class="container-fluid">
       <div class="row">
        <div class="col-10 offset-md-1">
          <AddNewTask @add-new-tasks="addNewTask" />
          <div class="card">
           <div class="card-body">
            <Tasks :tasks="openTasks" v-on:delete-task="deleteTask"/>
          </div>
         </div>
         <input type="checkbox" v-model="showCompletedTasks" id="show-comleted-tasks"> 
         <label for="show-completed-tasks" class="pl-2">Show Completed Tasks</label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
 import Tasks from "./components/Tasks.vue";
 import AddNewTask from "./components/AddNewTask.vue";

export default {
  name: 'App',
  components: {
    Tasks,
    AddNewTask
  },
  data() {
    return {
      tasks: [],
      showCompletedTasks: true
    }
  },
  methods: {
    deleteTask(id) {
     this.tasks = this.tasks.filter(task => task.id !== id);
     this.updateStorage(this.tasks);
     //fetch('https://jsonplaceholder.typicode.com/todos/${id}', { method: 'DELETE'})
     //.then(response => response.json())
     //.then(data => this.tasks.filter(task => task.id !== data.id))
     //.catch(e => console.log(e));
    },
    addNewTask(task) {
      this.tasks = [...this.tasks, task];
      this.updateStorage(this.tasks);
    },
    updateStorage(tasks) {
      localStorage.setItem('tasks', JSON.stringify(tasks));
    }
  },
  computed: {
    openTasks() {
      return this.showCompletedTasks ? this.tasks : this.tasks.filter(task => task.completed == false);
    }
  },
  mounted() {
    //const ls_tasks = localStorage.getItem('tasks');
    //if(ls_tasks !== null)
    //this.tasks = JSON.parse(ls_tasks);

    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(response => response.json())
    .then(data => this.tasks = data)
    .catch(e => console.log(e));
  }
}

</script>

<style>

</style>
