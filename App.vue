<script setup>
    import {ref, computed} from 'vue'

    const newTask = ref('')
    const hideCompleted = ref(false)
    const tasks = ref([])

    const filteredTasks = computed(() => {
      return hideCompleted.value
      ? tasks.value.filter((t) => !t.completed)
      : tasks.value
    })

    function addTask(){
        tasks.value.push({text: newTask.value, completed: false})
        newTask.value = ''
    }

    function removeTask(task){
      tasks.value = tasks.value.filter((t) => t !== task)
    }
</script>

<template>
    <div class="center">
        <form @submit.prevent="addTask">
            <input v-model="newTask" required placeholder="Enter task">
            <button>Add Task</button>
        </form>
        <ul>
            <li v-for="task in filteredTasks">
                <input type="checkbox" v-model="task.completed"/>
                <span :class="{completed: task.completed}">{{ task.text }}</span>
                <button @click="removeTask(task)">Delete Task</button>
            </li>
        </ul>
        <button @click="hideCompleted = !hideCompleted">
        {{ hideCompleted ? 'Show all' : 'Hide completed' }}
        </button>
    </div>

</template>

<style>
  .completed {
    text-decoration: line-through;
  }

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family:'Gill Sans', 'Gill Sans MT', Calibri, 'Trebuchet MS', sans-serif;
    background-color: #505081;
    color: white;
    font-size: 24px;   
}

.center {
    display: flex;
    align-items: center;
    flex-direction: column;
    margin-left: 25vw;
    margin-right: 25vw;
    background-color: #0f0e47;
    height: 100%;
    min-height:100vh;
}

form {
    margin-top: 25px;
    margin-bottom: 5px;
}

#task-input {
    margin-right: 3px;
}

#filter-btn {
    margin-top: 10px;
}

button {
    background-color: #0f0e47;
    border: solid 1px #505081;
    border-radius: 15px;
    color: white;
    padding: 5px;
    font-size: 20px;
}

button:hover {
    background-color: #505081;
}

.delete-task {
    margin-left: 10px;
}

</style>