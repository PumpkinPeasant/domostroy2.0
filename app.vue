<script lang="ts" setup>
import {useTodoStore} from "~~/store/todo";

const todoStore = useTodoStore();
const newTodo = ref('')
const error = ref(false)

watch(error, (value: boolean) => {
  if (value) {
    setTimeout(() => {
      error.value = false
    }, 3000)
  }
})

const saveNewTodo = () => {
  if (newTodo.value.length <= 0) {
    error.value = true
    return
  }

  todoStore.add({
    label: newTodo.value,
  })

  newTodo.value = '';

  console.log(todoStore.items)
}

</script>

<template>
  <div class="w-full min-h-screen bg-gray-100">
    <section class="text-center pt-7">
      <h1 class="text-4xl text-gray-800">Список дел на сегодня</h1>
    </section>
    <section class="w-9/12 max-w-lg mx-auto flex items-center justify-center mt-7 bg-white shadow p-5 rounded">
      <!--      <form action="">-->
      <!--        <input type="text" class="py-2 px-4 border border-blue-200 focus:outline-blue-300"-->
      <!--               placeholder="Добавить запись"/>-->
      <!--        <button class="border border-blue-200 py-2 px-4 ml-3 hover:bg-blue-50 transition-all duration-200 rounded">-->
      <!--          Добавить-->
      <!--        </button>-->
      <!--      </form>-->
      <todo-input v-model="newTodo" :error="error" @save="saveNewTodo"/>
      <todo-list :items="todoStore.items"/>
    </section>
  </div>
</template>
