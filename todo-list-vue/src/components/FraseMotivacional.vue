<template>
  <div class="frase">
    "{{ frase }}"
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'

export default {
  setup() {
    const frase = ref('Cargando frase motivacional...')

    onMounted(async () => {
      try {
        const res = await fetch('https://api.quotable.io/random')
        const data = await res.json()
        frase.value = data.content
      } catch (error) {
        frase.value = '¡Empieza tu día con una buena actitud!'
      }
    })

    return { frase }
  }
}
</script>

<style scoped>
.frase {
  font-style: italic;
  color: #555;
  margin-bottom: 1rem;
}
</style>
