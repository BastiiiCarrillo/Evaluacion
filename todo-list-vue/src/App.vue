<template>
  <div class="container">
    <h1>📝 Mi lista de tareas</h1>

    <FraseMotivacional />

    <FormularioTarea @agregar-tarea="agregarTarea" />

    <ListaTareas
      :tareas="tareas"
      @eliminar-tarea="eliminarTarea"
      @toggle-completada="toggleCompletada"
    />
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
import FormularioTarea from './components/FormularioTarea.vue'
import ListaTareas from './components/ListaTareas.vue'
import FraseMotivacional from './components/FraseMotivacional.vue'

export default {
  components: {
    FormularioTarea,
    ListaTareas,
    FraseMotivacional
  },
  setup() {
    const tareas = ref([])

    onMounted(() => {
      const guardadas = localStorage.getItem('tareas')
      if (guardadas) tareas.value = JSON.parse(guardadas)
    })

    const guardar = () => {
      localStorage.setItem('tareas', JSON.stringify(tareas.value))
    }

    const agregarTarea = (texto) => {
      tareas.value.push({ texto, completada: false })
      guardar()
    }

    const eliminarTarea = (index) => {
      tareas.value.splice(index, 1)
      guardar()
    }

    const toggleCompletada = (index) => {
      tareas.value[index].completada = !tareas.value[index].completada
      guardar()
    }

    return {
      tareas,
      agregarTarea,
      eliminarTarea,
      toggleCompletada
    }
  }
}
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 2rem auto;
  padding: 1rem;
  font-family: sans-serif;
}
</style>
