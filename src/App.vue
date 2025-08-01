<script>
import FormularioApp from './components/formulario.vue';

export default {
  name: "App",
  components: { FormularioApp }
}
</script>

<template>
  <div class="flex items-center justify-center flex-col bg-indigo-700 py-8">
    <h1 class="text-4xl font-bold text-white pb-6">Formulario</h1>
    <FormularioApp />
  </div>
</template>
