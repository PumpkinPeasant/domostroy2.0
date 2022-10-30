<script lang="ts" setup>
const props = defineProps<{
  modelValue: string,
  error: boolean
}>()

const emit = defineEmits<{
  (e: 'update:modelValue', value: string): void,
  (e: 'save'): void,
}>()

const localState = computed({
  get() {
    return props.modelValue
  },
  set(value: string) {
    emit('update:modelValue', value)
  }
})
</script>

<style scoped>

</style>

<template>
  <div class="todoInput">
    <input v-model="localState" type="text" class="py-2 px-4 border border-blue-200 focus:outline-blue-300"
           placeholder="Добавить запись"/>
    <button @click="$emit('save')"
            class="border border-blue-200 py-2 px-4 ml-3 hover:bg-blue-50 transition-all duration-200 rounded">
      Добавить
    </button>
  </div>
</template>
