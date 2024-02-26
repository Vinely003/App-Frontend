<template>
  <div id="hello">
    <h1>{{ msg }}</h1>
    <div v-for="data in datas" :key="data">
      <h2>Felhasználó: {{ data.name }}</h2>
      <h3>Üzenet: {{ data.message }}</h3>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: {
    msg: String,
  },
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
        .get(`http://127.0.0.1:8000/api/message`)
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
  background-color: yellowgreen;
  color: purple;
}
</style>
