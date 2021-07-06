<template>
    <div class="d-flex align-items-center">
       <input type="checkbox" v-model="task.completed" v-if="task.completed == false" />
       <span v-bind:class="{ completed: task.completed == true}">{{task.id }} - {{ task.title}}</span>
       <button v-on:click="$emit('delete-task', task.id)" class="btn btn-sm ml-4 btn-danger">x</button>
    </div>
</template>


<script>
export default {
    name:"Task",
    props: ["task"]
}

</script>

<style scoped>
.completed { text-decoration: line-through;}
</style>
