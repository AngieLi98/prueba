<template>
  <div>
    <h2 class="text-xl font-bold mb-4 text-indigo-700">
      Paso 2: Seguridad y contacto
    </h2>

    <!-- Email -->
    <label for="email">Correo electrónico</label>
    <div class="flex items-center mb-4">
      <input
        type="email"
        v-model="localForm.email"
        id="email"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      />
      <span class="ml-2" v-if="localForm.email">
        <span v-if="validEmail" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>

    <!-- Password -->
    <label for="password">Contraseña</label>
    <div class="flex items-center mb-4">
      <input
        type="password"
        v-model="localForm.password"
        id="password"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      />
      <span class="ml-2" v-if="localForm.password">
        <span v-if="validPassword" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>

    <!-- Confirm Password -->
    <label for="password-confirmation">Confirmación de Contraseña</label>
    <div class="flex items-center mb-4">
      <input
        type="password"
        v-model="localForm.passwordConfirm"
        id="password-confirmation"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      />
      <span class="ml-2" v-if="localForm.passwordConfirm">
        <span v-if="validPasswordConfirm" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>

    <!-- Teléfono -->
    <label for="telefono">Teléfono</label>
    <div class="flex items-center mb-4">
      <input
        type="tel"
        v-model="localForm.telefono"
        id="telefono"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      />
      <span class="ml-2" v-if="localForm.telefono">
        <span v-if="validTelefono" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>

    <!-- Celular -->
    <label for="celular">Celular</label>
    <div class="flex items-center">
      <input
        type="tel"
        v-model="localForm.celular"
        id="celular"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      />
      <span class="ml-2" v-if="localForm.celular">
        <span v-if="validCelular" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "PasoDos",
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
    validEmail() {
      return /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.localForm.email);
    },
    validPassword() {
      return this.localForm.password.length >= 6;
    },
    validPasswordConfirm() {
      return (
        this.localForm.passwordConfirm === this.localForm.password &&
        this.validPassword
      );
    },
    validTelefono() {
      return /^[0-9]{7,}$/.test(this.localForm.telefono);
    },
    validCelular() {
      return /^[0-9]{10,}$/.test(this.localForm.celular);
    },
    isValid() {
      return (
        this.validEmail &&
        this.validPassword &&
        this.validPasswordConfirm &&
        this.validTelefono &&
        this.validCelular
      );
    },
  },
  watch: {
    isValid(val) {
      this.$emit("valid-change", val);
    },
  },
};
</script>
