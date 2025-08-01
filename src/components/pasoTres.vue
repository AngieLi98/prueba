<template>
  <div>
    <h2 class="text-xl font-bold mb-4 text-indigo-700">Paso 3: Dirección</h2>

    <!-- Dirección -->
    <label for="direccion">Dirección residencia</label>
    <div class="flex items-center mb-4">
      <input
        type="text"
        v-model="localForm.direccion"
        id="direccion"
        class="border p-2 w-full"
      />
      <span class="ml-2" v-if="localForm.direccion">
        <span v-if="validDireccion" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>

    <!-- Código Postal -->
    <label for="codigo-postal">Código postal</label>
    <div class="flex items-center">
      <input
        type="text"
        v-model="localForm.codigoPostal"
        id="codigo-postal"
        class="border p-2 w-full"
      />
      <span class="ml-2" v-if="localForm.codigoPostal">
        <span v-if="validCodigoPostal" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "PasoTres",
  props: { modelValue: Object },
  computed: {
    localForm: {
      get() {
        return this.modelValue;
      },
      set(v) {
        this.$emit("update:modelValue", v);
      },
    },
    validDireccion() {
      return this.localForm.direccion.length > 3;
    },
    validCodigoPostal() {
      return /^[0-9]{4,10}$/.test(this.localForm.codigoPostal);
    },
    isValid() {
      return this.validDireccion && this.validCodigoPostal;
    },
  },
  watch: {
    isValid(val) {
      this.$emit("valid-change", val);
    },
  },
};
</script>
