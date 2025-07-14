<template>
  <ul>
    <li
      v-for="(tarea, index) in tareas"
      :key="index"
      class="flex justify-between items-center mb-2"
    >
      <span :class="{ 'line-through text-gray-500': tarea.completada }">
        {{ tarea.texto }}
      </span>
      <div class="space-x-2">
        <button @click="$emit('toggle-completada', index)" class="text-green-600">
          ✔
        </button>
        <button @click="$emit('eliminar-tarea', index)" class="text-red-500">
          ✘
        </button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  props: ['tareas']
}
</script>

<style scoped>
.line-through {
  text-decoration: line-through;
}
</style>
