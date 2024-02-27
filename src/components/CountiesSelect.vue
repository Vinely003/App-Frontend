<template>
  <h2 class="m-4">Megyék és Városaik</h2>
  <div class="input-group mx-auto d-flex justify-content-center">
    <label class="input-group-text" for="inputGroupSelect01"
      >Válassz egy megyét</label
    >
    <select class="form-select" v-model="county_id">
      <option :value="null" selected disabled>Megyék...</option>
      <option v-for="data in datas" :key="data.id" :value="data.id">
        {{ data.name }}
      </option>
    </select>
  </div>
  <div v-if="county_id !== null">
    <NewCities :county_id="county_id" />
  </div>
</template>

<script>
import axios from "axios";
import NewCities from "./NewCities.vue";

export default {
  components: {
    NewCities,
  },
  data() {
    return {
      datas: [],
      county_id: null,
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
