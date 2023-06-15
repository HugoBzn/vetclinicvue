<script setup>
import { ref, reactive } from "vue";
import Header from "./components/Header.vue";
import Formulario from "./components/Formulario.vue";

const pacientes = ref([]);

const pacienteState = reactive({
  nombre: "",
  propietario: "",
  email: "",
  alta: "",
  sintomas: "",
});

const guardarPaciente = () => {
  pacientes.value.push(pacienteState);
};
</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex">
      <Formulario
        v-model:nombre="pacienteState.nombre"
        v-model:propietario="pacienteState.propietario"
        v-model:email="pacienteState.email"
        v-model:alta="pacienteState.alta"
        v-model:sintomas="pacienteState.sintomas"
        @guardar-paciente="guardarPaciente"
      />

      <div class="md:w-1/2 md:h-screen overflow-y-auto">
        <h2 class="font-black text-2xl text-center">Administra tus pacientes</h2>

        <div v-if="pacientes.length > 0"></div>
        <div v-else>
          <p class="mt-20 text-2xl text-center">
            No hay <span class="text-violet-600 font-bold">Pacientes</span>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
