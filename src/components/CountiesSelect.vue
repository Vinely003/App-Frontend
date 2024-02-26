<template>
  <h2 class="m-4">Megyék és Városaik</h2>
  <div class="input-group mx-auto d-flex justify-content-center">
    <label class="input-group-text" for="inputGroupSelect01"
      >Válassz egy megyét</label
    >
    <select class="form-select">
      <option selected disabled>Megyék...</option>
      <option v-for="data in datas" :key="data">
        {{ data.name }}
      </option>
    </select>
  </div>
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
