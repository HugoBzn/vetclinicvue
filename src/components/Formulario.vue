<script setup>
import { reactive, computed } from "vue";
import Alerta from "./Alerta.vue";

const alertaState = reactive({
  tipo: "",
  mensaje: "",
});

const emit = defineEmits([
  "update:nombre",
  "update:propietario",
  "update:email",
  "update:alta",
  "update:sintomas",
  "guardar-paciente",
]);

const props = defineProps({
  id: {
    type: [String, null],
    required: true,
  },
  nombre: {
    type: String,
    required: true,
  },
  propietario: {
    type: String,
    required: true,
  },
  email: {
    type: String,
    required: true,
  },
  alta: {
    type: String,
    required: true,
  },
  sintomas: {
    type: String,
    required: true,
  },
});

const validar = () => {
  if (Object.values(props).includes("")) {
    alertaState.mensaje = "Todos los campos son obligatorios";
    alertaState.tipo = "error";
    return;
  }
  emit("guardar-paciente");
  alertaState.mensaje = "Paciente almacenado correctamente";
  alertaState.tipo = "exito";

  setTimeout(() => {
    Object.assign(alertaState, {
      tipo: "",
      mensaje: "",
    });
  }, 3000);
};

const editando = computed(() => {
  return props.id;
});
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-2xl text-center">Seguimiento pacientes</h2>
    <p class="text-lg mt-5 text-center mb-10">
      Añade pacientes y <span class="text-violet-600 font-bold">Adminístralos</span>
    </p>

    <Alerta v-if="alertaState.mensaje" :alerta="alertaState" />
    <form
      @submit.prevent="validar"
      class="bg-gray-900 rounded-lg py-10 px-5 mb-10 mx-5 border border-violet-600"
    >
      <div class="mb-5">
        <label for="mascota" class="block uppercase font-bold"> Nombre mascota </label>
        <input
          id="mascota"
          type="text"
          placeholder="Nombre de la mascota"
          class="border-2 w-full py-2 mt-2 placeholder-gray-400 rounded-md text-black"
          :value="nombre"
          @input="$emit('update:nombre', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="propietario" class="block uppercase font-bold"> Nombre propietario </label>
        <input
          id="propietario"
          type="text"
          placeholder="Nombre del propietario"
          class="border-2 w-full py-2 mt-2 placeholder-gray-400 rounded-md text-black"
          :value="propietario"
          @input="$emit('update:propietario', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="email" class="block uppercase font-bold"> Email </label>
        <input
          id="email"
          type="email"
          placeholder="Email"
          class="border-2 w-full py-2 mt-2 placeholder-gray-400 rounded-md text-black"
          :value="email"
          @input="$emit('update:email', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="alta" class="block uppercase font-bold"> Alta </label>
        <input
          id="alta"
          type="date"
          class="border-2 w-full py-2 mt-2 placeholder-gray-400 rounded-md text-black"
          :value="alta"
          @input="$emit('update:alta', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="sintomas" class="block uppercase font-bold"> Síntomas </label>
        <textarea
          id="sintomas"
          placeholder="Describe los síntomas"
          class="border-2 w-full py-2 mt-2 placeholder-gray-400 rounded-md text-black h-40"
          :value="sintomas"
          @input="$emit('update:sintomas', $event.target.value)"
        />
      </div>

      <input
        type="submit"
        class="bg-violet-600 rounded-md w-full p-3 text-white uppercase font-bold hover:bg-violet-700 cursor-pointer transition-colors"
        :value="[editando ? 'Guardar cambios' : 'Registrar paciente']"
      />
    </form>
  </div>
</template>
