<template>
  <form @submit.prevent="enviar" class="formulario">
    <input
      v-model="nuevaTarea"
      type="text"
      placeholder="Escribe una tarea..."
      required
    />
    <button>Agregar</button>
  </form>
</template>

<script>
import { ref } from 'vue'

export default {
  emits: ['agregar-tarea'],
  setup(_, { emit }) {
    const nuevaTarea = ref('')

    const enviar = () => {
      if (nuevaTarea.value.trim() === '') return
      emit('agregar-tarea', nuevaTarea.value)
      nuevaTarea.value = ''
    }

    return { nuevaTarea, enviar }
  }
}
</script>

<style scoped>
.formulario {
  display: flex;
  gap: 0.5rem;
  margin-bottom: 1rem;
}
input {
  flex: 1;
  padding: 0.5rem;
  font-size: 1rem;
}
button {
  padding: 0.5rem 1rem;
  font-size: 1rem;
  background-color: #007bff;
  color: white;
  border: none;
  cursor: pointer;
}
</style>
