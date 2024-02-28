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
  <transition @beforeEnter="beforeEnter" @enter="enter">
    <div v-if="county_id !== null">
      <CityTable :county_id="county_id" />
    </div>
  </transition>
</template>

<script>
import axios from "axios";
import CityTable from "./CityTable.vue";

export default {
  components: {
    CityTable,
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
    beforeEnter(el) {
      el.style.opacity = 0;
    },
    enter(el, done) {
      let opacity = 0;
      const interval = setInterval(() => {
        el.style.opacity = opacity;
        opacity += 0.1;
        if (opacity >= 1) {
          clearInterval(interval);
          done();
        }
      }, 60);
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
