<template>
  <div class="flex justify-between mb-6">
    <div v-for="n in 3" :key="n" class="flex-1 text-center">
      <div
        :class="[
          'w-10 h-10 mx-auto rounded-full flex items-center justify-center',
          step >= n ? 'bg-blue-400 text-white' : 'bg-gray-300 text-gray-700'
        ]"
      >
        {{ n }}
      </div>
      <p :class="step >= n ? 'font-bold text-blue-700' : 'text-gray-500'">
        Paso {{ n }}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: "LineaDelTiempo",
  props: {
    step: {
      type: Number,
      required: true
    }
  }
}
</script>
