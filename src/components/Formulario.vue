<script setup>
import { reactive } from "vue";
import Alerta from "./Alerta.vue";

const alertaState = reactive({
  mensaje: "",
  tipo: "",
});

const pacienteState = reactive({
  nombre: "",
  propietario: "",
  email: "",
  alta: "",
  sintomas: "",
});

const validar = () => {
  if (Object.values(pacienteState).includes("")) {
    alertaState.mensaje = "Todos los campos son obligatorios";
    alertaState.tipo = "error";
    return;
  }
  console.log("Despues del IF");
};
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="font-black text-2xl text-center">Seguimiento pacientes</h2>
    <p class="text-lg mt-5 text-center mb-10">
      Añade pacientes <span class="text-violet-600 font-bold">Adminístralos</span>
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
          class="border-2 w-full pt-2 mt-2 placeholder-gray-400 rounded-md text-black"
          v-model="pacienteState.nombre"
        />
      </div>

      <div class="mb-5">
        <label for="propietario" class="block uppercase font-bold"> Nombre propietario </label>
        <input
          id="propietario"
          type="text"
          placeholder="Nombre del propietario"
          class="border-2 w-full pt-2 mt-2 placeholder-gray-400 rounded-md text-black"
          v-model="pacienteState.propietario"
        />
      </div>

      <div class="mb-5">
        <label for="email" class="block uppercase font-bold"> Email </label>
        <input
          id="email"
          type="email"
          placeholder="Email"
          class="border-2 w-full pt-2 mt-2 placeholder-gray-400 rounded-md text-black"
          v-model="pacienteState.email"
        />
      </div>

      <div class="mb-5">
        <label for="alta" class="block uppercase font-bold"> Alta </label>
        <input
          id="alta"
          type="date"
          class="border-2 w-full pt-2 mt-2 placeholder-gray-400 rounded-md text-black"
          v-model="pacienteState.alta"
        />
      </div>

      <div class="mb-5">
        <label for="sintomas" class="block uppercase font-bold"> Síntomas </label>
        <textarea
          id="sintomas"
          placeholder="Describe los síntomas"
          class="border-2 w-full pt-2 mt-2 placeholder-gray-400 rounded-md text-black h-40"
          v-model="pacienteState.sintomas"
        />
      </div>

      <input
        type="submit"
        class="bg-violet-600 rounded-md w-full p-3 text-white uppercase font-bold hover:bg-violet-700 cursor-pointer transition-colors"
        value="Registrar paciente"
      />
    </form>
  </div>
</template>
