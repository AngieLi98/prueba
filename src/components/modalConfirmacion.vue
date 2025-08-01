<template>
  <div v-if="show" class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50">
    <div class="bg-white p-6 rounded-lg shadow-lg w-96 text-center">
      <h2 class="text-xl font-bold mb-4">✅ Formulario enviado</h2>
      <p class="mb-4">Tu formulario se ha enviado correctamente.</p>
      <button @click="$emit('close')" class="bg-indigo-700 text-white px-4 py-2 rounded">
        Cerrar
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModalConfirmacion",
  props: { show: { type: Boolean, default: false } }
}

</script>
