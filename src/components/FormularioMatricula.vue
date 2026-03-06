<template>
  <div class="container">
    <h2>Matrícula em Cursos</h2>

    <form @submit.prevent="enviarFormulario">
      <div>
        <label>Nome Completo</label>
        <input v-model="nomeCompleto" type="text" />
        <span v-if="erroNome">{{ erroNome }}</span>
      </div>

      <div>
        <label>E-mail</label>
        <input v-model="email" type="email" />
        <span v-if="erroEmail">{{ erroEmail }}</span>
      </div>

      <div>
        <label>Curso</label>
        <select v-model="cursoSelecionado">
          <option value="">Selecione um curso</option>
          <option v-for="curso in cursos" :key="curso.id" :value="curso.id">
            {{ curso.nome }}
          </option>
        </select>
      </div>

      <button :disabled="carregando">
        {{ carregando ? "Enviando..." : "Realizar Matrícula" }}
      </button>
    </form>

    <p v-if="mensagemSucesso" class="sucesso">{{ mensagemSucesso }}</p>
    <p v-if="mensagemErro" class="erro">{{ mensagemErro }}</p>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";

const nomeCompleto = ref("");
const email = ref("");
const cursoSelecionado = ref("");
const cursos = ref([]);

const erroNome = ref("");
const erroEmail = ref("");

const mensagemSucesso = ref("");
const mensagemErro = ref("");
const carregando = ref(false);

onMounted(async () => {
  const response = await axios.get("<http://localhost:3000/cursos>");
  cursos.value = response.data;
});

const validar = () => {
  erroNome.value = nomeCompleto.value ? "" : "Nome é obrigatório";
  erroEmail.value = email.value.includes("@") ? "" : "E-mail inválido";

  return !erroNome.value && !erroEmail.value;
};

const enviarFormulario = async () => {
  if (!validar()) return;

  carregando.value = true;
  mensagemErro.value = "";
  mensagemSucesso.value = "";

  try {
    const response = await axios.post("<http://localhost:3000/matricula>", {
      nomeCompleto: nomeCompleto.value,
      email: email.value,
      cursoId: Number(cursoSelecionado.value)
    });

    mensagemSucesso.value = response.data.message;
  } catch (error) {
    mensagemErro.value = error.response?.data?.message || "Erro ao enviar";
  } finally {
    carregando.value = false;
  }
};
</script>

<style>
.container {
  max-width: 400px;
  margin: auto;
}
.erro {
  color: red;
}
.sucesso {
  color: green;
}
</style>