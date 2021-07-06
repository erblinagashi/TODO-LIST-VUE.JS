<template>
    <div> 
        <input type="text" class="form-control my-2" placeholder="Enter task here..." v-model="title" @keyup.enter="addNewTask" />
    </div>
</template>

<script> 
import { v4 } from 'uuid';
export default {
    name: "AddNewTask",
    data () {
        return {
            title : ''
        }
    },
    methods: {
        addNewTask () {
            const task = {
                id: v4(),
                title: this.title,
                completed: false
            };
            this.$emit('add-new-task', task);
            this.title = '';
        }
    }
}

</script>

<style  scoped>

</style>