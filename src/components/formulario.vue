<script>
import PasoUno from "./pasoUno.vue";
import PasoDos from "./pasoDos.vue";
import PasoTres from "./pasoTres.vue";
import LineaDelTiempo from "./lineaDelTiempo.vue";
import ModalConfirmacion from "./modalConfirmacion.vue";

export default {
  name: "FormularioApp",
  components: { PasoUno, PasoDos, PasoTres, LineaDelTiempo, ModalConfirmacion },
  data() {
    return {
      step: 1,
      validStep1: false,
      validStep2: false,
      validStep3: false,
      showModal: false,
      formData: {
        pais: "",
        genero: "",
        primerNombre: "",
        segundoNombre: "",
        nacimiento: "",
        tipoDocumento: "",
        numeroDocumento: "",
        documentoFrente: null,
        documentoReverso: null,
        email: "",
        password: "",
        passwordConfirm: "",
        telefono: "",
        celular: "",
        direccion: "",
        codigoPostal: "",
      },
    };
  },
  computed: {
    isStepValid() {
      if (this.step === 1) return this.validStep1;
      if (this.step === 2) return this.validStep2;
      if (this.step === 3) return this.validStep3;
      return false;
    },
  },
  methods: {
    nextStep() {
      if (this.step < 3) this.step++;
    },
    prevStep() {
      if (this.step > 1) this.step--;
    },
    handleSubmit() {
      console.log("📌 Datos del formulario:", { ...this.formData });
      this.showModal = true;
    },
  },
};
</script>

<template>
  <div class="p-10 bg-white shadow-md rounded-lg w-5/6 h-auto">
    <!-- Línea del tiempo -->
    <LineaDelTiempo :step="step" />

    <!-- Paso 1 -->
    <div v-if="step === 1">
      <PasoUno v-model="formData" @valid-change="validStep1 = $event" />
      <div class="flex justify-end mt-4">
        <button
          @click="nextStep"
          :disabled="!isStepValid"
          class="bg-blue-400 hover:bg-indigo-700 text-white px-4 py-2 rounded disabled:opacity-50"
        >
          Siguiente
        </button>
      </div>
    </div>

    <!-- Paso 2 -->
    <div v-if="step === 2">
      <PasoDos v-model="formData" @valid-change="validStep2 = $event" />
      <div class="flex justify-between mt-4">
        <button
          @click="prevStep"
          class="bg-gray-700 hover:bg-gray-400 text-white px-4 py-2 rounded"
        >
          Atrás
        </button>
        <button
          @click="nextStep"
          :disabled="!isStepValid"
          class="bg-blue-400 hover:bg-indigo-700 text-white px-4 py-2 rounded disabled:opacity-50"
        >
          Siguiente
        </button>
      </div>
    </div>

    <!-- Paso 3 -->
    <div v-if="step === 3">
      <PasoTres v-model="formData" @valid-change="validStep3 = $event" />
      <div class="flex justify-between mt-4">
        <button
          @click="prevStep"
          class="bg-gray-700 hover:bg-gray-400 text-white px-4 py-2 rounded"
        >
          Atrás
        </button>
        <button
          @click="handleSubmit"
          :disabled="!isStepValid"
          class="bg-blue-400 hover:bg-indigo-700 text-white px-4 py-2 rounded border-4 disabled:opacity-50"
        >
          Enviar
        </button>
      </div>
    </div>

    <!-- Modal de confirmación -->
    <ModalConfirmacion :show="showModal" @close="showModal = false" />
  </div>
</template>
