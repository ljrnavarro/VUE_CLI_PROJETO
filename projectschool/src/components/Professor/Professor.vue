<template>
  <div>
    <h1>
      <titulo texto="Professor" />
    </h1>
    <table>
      <thead>
        <th>Código</th>
        <th>Nome</th>
        <th>Qnt. Alunos</th>
      </thead>
      <tbody v-if="professores.length">
        <tr v-for="(professor, index) in professores" :key="index">
          <td>{{ professor.id }}</td>

          <router-link to="/alunos/" tag="td" style="cursor: pointer">
            {{ professor.nome }} {{ professor.sobrenome }}
          </router-link>

          <td>
            {{getQtdAlunosPorProfessor(professor.id)}}
          </td>
        </tr>
      </tbody>
      <tfoot v-else>
        Nenhum registro encontrado...
      </tfoot>
    </table>
  </div>
</template>

<script>
import Titulo from "../_share/Titulo";
import VueResource from "vue-resource";
export default {
  components: {
    Titulo,
  },
  data() {
    return {
      professores: [],
      alunos: []
    };
  },
  created() {
   this.$http
      .get("http://localhost:3000/alunos")
      .then((res) => res.json())
      .then((alunos) => {
        this.alunos = alunos;
        this.carregarProfessores();
        });
  },
  props: {},
  methods: {
    getQtdAlunosPorProfessor(id) {
          return this.alunos.filter(aluno => 
          aluno.professor.id == id
          ).length;
        },
    carregarProfessores() {
      this.$http
        .get("http://localhost:3000/professores")
        .then((res) => res.json())
        .then((professor) => {
          this.professores = professor;
          });
    },
  },
};
</script>

<style lang="scss" scoped></style>
