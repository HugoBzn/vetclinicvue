<script setup>
import { ref, reactive, onMounted, watch } from "vue";
import { uid } from "uid";
import Header from "./components/Header.vue";
import Formulario from "./components/Formulario.vue";
import Paciente from "./components/Paciente.vue";

const pacientes = ref([]);

const paciente = reactive({
  id: null,
  nombre: "",
  propietario: "",
  email: "",
  alta: "",
  sintomas: "",
});

watch(
  pacientes,
  () => {
    guardarLocalStorage();
  },
  { deep: true }
);

const guardarLocalStorage = () => {
  localStorage.setItem("pacientes", JSON.stringify(pacientes.value));
};

onMounted(() => {
  const pacientesStorage = localStorage.getItem("pacientes");
  if (pacientesStorage) {
    pacientes.value = JSON.parse(pacientesStorage);
  }
});

const guardarPaciente = () => {
  if (paciente.id) {
    const { id } = paciente;
    const i = pacientes.value.findIndex((paciente) => paciente.id === id);
    pacientes.value[i] = { ...paciente };
  } else {
    pacientes.value.push({ ...paciente, id: uid() });
  }

  // Reset form
  Object.assign(paciente, {
    nombre: "",
    propietario: "",
    email: "",
    alta: "",
    sintomas: "",
    id: null,
  });
};

const actualizarPaciente = (id) => {
  const pacienteEditar = pacientes.value.filter((paciente) => paciente.id === id)[0];
  Object.assign(paciente, pacienteEditar);
};

const eliminarPaciente = (id) => {
  pacientes.value = pacientes.value.filter((paciente) => paciente.id !== id);
};
</script>

<template>
  <div class="container mx-auto mt-20">
    <Header />

    <div class="mt-12 md:flex">
      <Formulario
        v-model:nombre="paciente.nombre"
        v-model:propietario="paciente.propietario"
        v-model:email="paciente.email"
        v-model:alta="paciente.alta"
        v-model:sintomas="paciente.sintomas"
        @guardar-paciente="guardarPaciente"
        :id="paciente.id"
      />

      <div class="md:w-1/2">
        <h2 class="font-black text-2xl text-center">Administra tus pacientes</h2>
        <p class="text-lg mt-5 text-center">
          Información de <span class="text-violet-600 font-bold">Pacientes</span>
        </p>
        <div class="overflow-y-scroll" style="height: 50rem">
          <div v-if="pacientes.length > 0">
            <Paciente
              v-for="paciente in pacientes"
              :key="paciente.id"
              :paciente="paciente"
              @actualizar-paciente="actualizarPaciente"
              @eliminar-paciente="eliminarPaciente"
            />
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
