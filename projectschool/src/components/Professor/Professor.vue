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
            3
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
      professores: [
        { id: 1, nome: "Vinicius", sobrenome: "Silva" },
        { id: 2, nome: "Francisco", sobrenome: "Xavier" },
        { id: 3, nome: "Luis", sobrenome: "Dantas" }
      ]
    };
  }
};
</script>

<style lang="scss" scoped></style>
