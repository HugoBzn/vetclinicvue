<script setup>
defineProps({
  paciente: {
    type: Object,
    required: true,
  },
});

defineEmits(["actualizar-paciente", "eliminar-paciente"]);
</script>

<template>
  <div class="bg-gray-900 rounded-lg mx-5 my-10 px-5 py-10 border border-violet-600">
    <p class="font-bold mb-3 uppercase">
      ID:
      <span class="font-normal normal-case"> {{ paciente.id }} </span>
    </p>

    <p class="font-bold mb-3 uppercase">
      Nombre:
      <span class="font-normal normal-case"> {{ paciente.nombre }} </span>
    </p>

    <p class="font-bold mb-3 uppercase">
      Propietario:
      <span class="font-normal normal-case"> {{ paciente.propietario }} </span>
    </p>

    <p class="font-bold mb-3 uppercase">
      Email:
      <span class="font-normal normal-case"> {{ paciente.email }} </span>
    </p>

    <p class="font-bold mb-3 uppercase">
      Fecha Alta:
      <span class="font-normal normal-case"> {{ paciente.alta }} </span>
    </p>

    <p class="font-bold mb-3 uppercase">
      Síntomas:
      <span class="font-normal normal-case"> {{ paciente.sintomas }} </span>
    </p>

    <div class="grid md:grid-cols-2 gap-5 mt-10">
      <button
        type="button"
        class="block w-full py-2 px-10 bg-violet-600 hover:bg-violet-700 font-bold uppercase rounded-lg"
        @click="$emit('actualizar-paciente', paciente.id)"
      >
        Editar
      </button>

      <button
        type="button"
        class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 font-bold uppercase rounded-lg"
        @click="$emit('eliminar-paciente', paciente.id)"
      >
        Eliminar
      </button>
    </div>
  </div>
</template>
