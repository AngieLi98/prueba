<template>
  <div>
    <h2 class="text-xl font-bold mb-4 text-indigo-700">
      Paso 1: Datos personales
    </h2>

    <!-- País -->
    <label for="pais">País</label>
    <div class="flex items-center mb-4">
      <select
        v-model="localForm.pais"
        id="pais"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      >
        <option disabled value="">Selecciona un país</option>
        <option v-for="pais in paises" :key="pais.code" :value="pais.name">
          {{ pais.name }}
        </option>
      </select>
      <span class="ml-2" v-if="localForm.pais">
        <span v-if="validPais" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>

    <!-- Género -->
    <label for="genero">Género</label>
    <div class="flex items-center mb-4">
      <select
        v-model="localForm.genero"
        id="genero"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      >
        <option disabled value="">Elige</option>
        <option value="F">Femenino</option>
        <option value="M">Masculino</option>
      </select>
      <span class="ml-2" v-if="localForm.genero">
        <span v-if="validGenero" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>

    <!-- Primer Nombre -->
    <label for="primer-nombre">Primer Nombre</label>
    <div class="flex items-center mb-4">
      <input
        type="text"
        v-model="localForm.primerNombre"
        id="primer-nombre"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      />
      <span class="ml-2" v-if="localForm.primerNombre">
        <span v-if="validPrimerNombre" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>

    <!-- Segundo Nombre -->
    <label for="segundo-nombre">Segundo Nombre</label>
    <div class="flex items-center mb-4">
      <input
        type="text"
        v-model="localForm.segundoNombre"
        id="segundo-nombre"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      />
      <span class="ml-2" v-if="localForm.segundoNombre">
        <span v-if="validSegundoNombre" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>

    <!-- Fecha nacimiento -->
    <label for="nacimiento">Fecha de nacimiento</label>
    <div class="flex items-center mb-4">
      <input
        type="date"
        v-model="localForm.nacimiento"
        id="nacimiento"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      />
      <span class="ml-2" v-if="localForm.nacimiento">
        <span v-if="validEdad" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>

    <!-- Tipo Documento -->
    <label for="documento">Tipo de documento</label>
    <div class="flex items-center mb-4">
      <select
        v-model="localForm.tipoDocumento"
        id="documento"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      >
        <option disabled value="">Elige</option>
        <option value="cedula-ciudadania">Cédula de ciudadanía</option>
        <option value="pasaporte">Pasaporte</option>
        <option value="cedula-extranjeria">Cédula de extranjería</option>
      </select>
      <span class="ml-2" v-if="localForm.tipoDocumento">
        <span v-if="validTipoDocumento" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>

    <!-- Número Documento -->
    <label for="numero-documento">Número documento</label>
    <div class="flex items-center">
      <input
        type="number"
        v-model="localForm.numeroDocumento"
        id="numero-documento"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      />
      <span class="ml-2" v-if="localForm.numeroDocumento">
        <span v-if="validDocumento" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>

    <!-- Documento Frente -->
    <h3 class="py-4">Documetos formato JPG</h3>
    <label for="documento-frente">Foto documento - Frente</label>
    <div class="flex items-center mb-4">
      <input
        type="file"
        @change="(e) => (localForm.documentoFrente = e.target.files[0])"
        id="documento-frente"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      />
      <span class="ml-2" v-if="localForm.documentoFrente">
        <span v-if="validDocumentoFrente" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>

    <!-- Documento Reverso -->
    <label for="documento-reverso">Foto documento - Reverso</label>
    <div class="flex items-center">
      <input
        type="file"
        @change="(e) => (localForm.documentoReverso = e.target.files[0])"
        id="documento-reverso"
        class="border-4 border-indigo-400 focus:border-indigo-700 rounded-lg p-2 w-11/12"
      />
      <span class="ml-2" v-if="localForm.documentoReverso">
        <span v-if="validDocumentoReverso" class="text-green-500">✅</span>
        <span v-else class="text-red-500">❌</span>
      </span>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "PasoUno",
  props: { modelValue: Object },
  data() {
    return {
      paises: [], 
    };
  },
  computed: {
    localForm: {
      get() {
        return this.modelValue;
      },
      set(v) {
        this.$emit("update:modelValue", v);
      },
    },
    validPais() {
      return this.localForm.pais !== "";
    },
    validGenero() {
      return this.localForm.genero !== "";
    },
    validPrimerNombre() {
      return this.localForm.primerNombre.length > 1;
    },
    validSegundoNombre() {
      return this.localForm.segundoNombre.length > 1;
    },
    validEdad() {
      if (!this.localForm.nacimiento) return false;
      const hoy = new Date();
      const cumple = new Date(this.localForm.nacimiento);
      let edad = hoy.getFullYear() - cumple.getFullYear();
      const m = hoy.getMonth() - cumple.getMonth();
      if (m < 0 || (m === 0 && hoy.getDate() < cumple.getDate())) edad--;
      return edad >= 18;
    },
    validTipoDocumento() {
      return this.localForm.tipoDocumento !== "";
    },
    validDocumento() {
      return /^[0-9]{5,}$/.test(this.localForm.numeroDocumento);
    },
    validDocumentoFrente() {
      return this.localForm.documentoFrente instanceof File;
    },
    validDocumentoReverso() {
      return this.localForm.documentoReverso instanceof File;
    },
    isValid() {
      return (
        this.validPais &&
        this.validGenero &&
        this.validPrimerNombre &&
        this.validSegundoNombre &&
        this.validEdad &&
        this.validTipoDocumento &&
        this.validDocumento &&
        this.validDocumentoFrente &&
        this.validDocumentoReverso
      );
    },
  },
  watch: {
    isValid(val) {
      this.$emit("valid-change", val);
    },
  },
  methods: {
    async fetchPaises() {
      try {
        
        const res = await axios.get(
          "https://restcountries.com/v3.1/all?fields=name,cca2"
        );

        this.paises = res.data
          .map((p) => ({
            name: p.name.common,
            code: p.cca2,
          }))
          .sort((a, b) => a.name.localeCompare(b.name));
      } catch (err) {
        console.error("❌ Error cargando países:", err.message);
      }
    },
  },
  mounted() {
    this.fetchPaises(); 
  },
};
</script>
