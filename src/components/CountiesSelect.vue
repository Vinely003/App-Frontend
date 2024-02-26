<template>
  <h1>Megyek és Városai</h1>
  <select class="form-select" aria-label="Default select example">
    <option selected disabled>Válassz egy megyét...</option>
    <option v-for="data in datas" :key="data">{{ data.name }}</option>
  </select>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      datas: [],
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      axios
        .get(`http://127.0.0.1:8000/api/counties`)
        .then((response) => {
          this.datas = response.data.data;
        })
        .catch((error) => {
          console.error("Hiba történt:", error);
        });
    },
  },
};
</script>

<style scoped>
#hello {
  font-size: 25px;
  background-color: lightgreen;
  color: purple;
}
</style>
