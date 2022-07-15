<script>
  import axios from "axios";
  export default {
    data() {
      return {
        times: [],
        time: {},
      };
    },
    async created() {
      const times = await axios.get("http://localhost:4000/times/");
      this.times = times.data;
    },
    methods: {
      async salvar() {
        if (this.times.id) {
          const time_alterado = await axios.put(
            `http://localhost:4000/times/${this.time.id}`,
            this.time
          );
        } else {
          const time_criado = await axios.post(
            "http://localhost:4000/times/",
            this.time
          );
          this.times.push(time_criado.data);
        }
      },
      async excluir(time) {
        await axios.delete(`http://localhost:4000/times/${time.id}`);
        const indice = this.times.indexOf(time);
        this.times.splice(indice, 1);
      },
    },
  };
</script>
<template>
  <main>
    <div class="container">
      <div class="title">
        <h2>Gerenciamento de Times</h2>
      </div>
      <div class="form-input">
        <input type="text" v-model="time.nome" />
        <button @click="salvar">Salvar</button>
      </div>
      <div class="list-times">
        <table>
          <thead>
            <tr>
              <th>ID</th>
              <th>Nome</th>
              <th>Ações</th>
              <th>Estádios</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="time in times" :key="time.id">
              <td>{{ time.id }}</td>
              <td>{{ time.nome }}</td>
              <td>
                <button>editar</button>
                <button @click="excluir(time)">excluir</button>
              </td>
              <td>{{ time.estadio }}</td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </main>
</template>
<style>
  .title {
    display: flex;
    justify-content: center;
    margin-top: 30px;
  }
  .form-input {
    margin-top: 10px;
    display: flex;
    justify-content: center;
  }
  .form-input input {
    width: 60%;
    height: 40px;
    border: 1px solid rgb(147, 147, 147);
    border-radius: 10px;
    padding: 0 10px;
  }
  .form-input button {
    margin-left: 1px;
    width: 20%;
    height: 40px;
    border: 1px solid rgb(211, 211, 211);
    border-radius: 10px;
    color: rgb(255, 255, 255);
    font-weight: bold;
    cursor: pointer;
  }
  .list-times {
    display: flex;
    justify-content: center;
  }
  .list-times table {
    width: 80%;
    margin: 0 auto;
    border-collapse: collapse;
  }
  table tr td {
    border: 1px solid rgb(211, 211, 211);
    padding: 10px;
  }
</style>
