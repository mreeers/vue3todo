<template>
  <main>
    <TaskInput @onAddTask="addTask"></TaskInput>
    <ul class="my-list task-list">
      <li v-for="item in taskList" :key="item.id">
        <TaskCart @onRemove="removeTask(item.id)"  @onDone="setDoneTask(item.id)" :model="item"></TaskCart>
      </li>
    </ul>
  </main>
</template>

<script>

import TaskCart from "./components/TaskCart.vue";
import TaskInput from "./components/TaskInput.vue";
import {ref} from 'vue';

export default {
  name: 'App',
  components: {
    TaskCart,
    TaskInput
  },
  setup() {
    const taskList = ref([{id: 0, title: 'Create task', description: 'description test', status: false}])

    const addTask = ({title, description}) => {
      taskList.value = [...taskList.value, {id: taskList.value[taskList.value - 1].id + 1, title, description, status: false}]
    }

    const setDoneTask = (id) => {
      taskList.value = taskList.value.map(x => {
        if(x.id === id)
          x.status = true
        return x;
      })
    }
    const removeTask = (id) => {
      taskList.value = taskList.value.filter(x => x.id !== id);
    }

    return {
      taskList,
      addTask,
      removeTask,
      setDoneTask
    }
  }
}
</script>

<style scoped>
  .task-list {
    list-style: none;
  }
</style>