<template>
  <div>
    <h1>
      <titulo texto="Aluno" />
    </h1>
    <div>
      <input
        type="text"
        style="border-style: solid; border-width: 1px"
        placeholder="Nome do Aluno"
        v-model="nome"
        @keyup.enter="addAluno()"
      /> 
       <input
        type="text"
        style="border-style: solid; border-width: 1px; margin-left: 5px"
        placeholder="Sobrenome"
        v-model="sobrenome"
        @keyup.enter="addAluno()"
      />
      <button class="btn btn_Input" @click="addAluno()">Adicionar</button>
    </div>

    <table>
      <thead>
        <th>Mat.</th>
        <th>Aluno</th>
        <th>Opções</th>
      </thead>
      <tbody v-if="alunos.length">
        <tr v-for="(aluno, index) in alunos" :key="index">
          <td>{{ aluno.id }}</td>
          <td>{{ aluno.nome }} {{ aluno.sobrenome }}</td>
          <td>
            <button class="btn btn_Danger" @click="remover(aluno)">
              Remover
            </button>
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
    Titulo
  },
  data() {
    return {
      titulo: "Aluno",
      nome: "",
      sobrenome: "",
      alunos: []
    };
  },
  created() {
    this.$http
      .get("http://localhost:3000/alunos")
      .then((res) => res.json())
      .then((alunos) => (this.alunos = alunos));
  },
  props: {},
  methods: {
    addAluno() {
      let _aluno = {
        nome: this.nome,
        sobrenome: this.sobrenome
      };

      this.$http
        .post("http://localhost:3000/alunos", _aluno)
        .then((res) => res.json())
        .then((alunoRet) => {
          this.alunos.push(alunoRet);
          this.nome = this.sobrenome = "";
        });
      this.nome = "";
    },
    remover(aluno) {
      this.$http.delete(`http://localhost:3000/alunos/${aluno.id}`).then(() => {
        let indice = this.alunos.indexOf(aluno);
        this.alunos.splice(indice, 1);
      });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input {
  border: 0;
  padding: 20px;
  font-size: 1.3em;
  color: #687f7f;
  display: inline;
}

.btn_Input {
  border: 0px;
  padding: 20px;
  font-size: 1.3em;
  display: inline;
  background-color: rgb(116, 115, 115);
}

.btn_Input:hover {
  padding: 20px;
  margin: 0px;
  border: 0px;
}
</style>
