<script setup>
import { ref } from 'vue'

const tasks = ref([])
const newTask = ref('')
const dueDate = ref('')

function deleteTask(task){
  tasks.value.splice(tasks.value.indexOf(task), 1)
}

function handleSubmit(){
  tasks.value.push({
    id: Date.now(),
    done: false,
    title: newTask.value,
    date: dueDate.value,
  })
  newTask.value = ""
  dueDate.value = ""
}

</script>

<template>
  <div class="border-[1px] rounded-md border-zinc-400 w-96 p-2.5 mx-auto mt-28">
    <div>
      <form @submit.prevent="handleSubmit">
        <div class="text-center">
          <h1 class="text-2xl font-light">TODOs</h1>
        </div>
        <div class="flex flex-col">
          <input v-model="newTask" name="newTask" placeholder="Enter a task"
                 class="mt-1 py-1.5 px-2 bg-zinc-50 focus:outline-[1px] focus:outline-stone-200">
        </div>
        <div class="my-1.5 flex flex-row items-center">
          <h3 class="mr-2">Due Date:</h3>
          <input type="date" v-model="dueDate"
                 class="bg-zinc-50 px-1 items-center focus:outline-[1px] focus:outline-stone-200"/>
        </div>
        <button type="submit"
                class="my-1 w-[100%] bg-blue-300 hover:bg-blue-200 text-blue-900 transition-all duration-200 ease-in-out">
          Add Todo
        </button>
      </form>
    </div>
    <main>
      <div>
        <h2 class="mt-4 text-center text-xl font-light">You have <span class="text-emerald-700">{{ tasks.length }}</span> TODOs</h2>
        <div v-for="task in tasks" key="task.id" class="p-2 my-3 bg-stone-100 rounded border-stone-600 border-[1px]">
          <div class="flex flex-col">
            <h4>{{ task.title }}</h4>
            <div class="flex flex-row justify-between">
              <span class="text-stone-500 font-light">{{ task.date }}</span>
              <button @click="deleteTask(task)"
                      class="bg-red-400 px-1.5 py-.5 rounded-[5px] hover:bg-red-300 transition-all duration-200 ease-in-out">
                Delete</button>
            </div>
          </div>
        </div>
        <div>
        </div>
      </div>
    </main>
  </div>
</template>

