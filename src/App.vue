<script setup>
import { ref, reactive } from "vue";
import Header from "./components/Header.vue";
import Formulario from "./components/Formulario.vue";
import Paciente from "./components/Paciente.vue";

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

      <div class="md:w-1/2">
        <h2 class="font-black text-2xl text-center">Administra tus pacientes</h2>
        <p class="text-lg mt-5 text-center">
          Información de <span class="text-violet-600 font-bold">Pacientes</span>
        </p>
        <div class="overflow-y-scroll" style="height: 50rem">
          <div v-if="pacientes.length > 0">
            <Paciente v-for="paciente in pacientes" :paciente="paciente" />
          </div>
          <div v-else>
            <p class="mt-10 text-2xl text-center pb-10">
              No hay <span class="text-violet-600 font-bold">Pacientes</span>
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="css">
@media (min-width: 768px) {
  pacientes {
    height: 75rem;
  }
}
</style>
