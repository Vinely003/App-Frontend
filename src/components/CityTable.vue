<template>
  <table class="table table-striped mx-auto" style="width: 45%">
    <tbody>
      <tr v-for="data in filteredCities" :key="data.id">
        <th scope="row">
          {{ data.name }}
        </th>
      </tr>
    </tbody>
  </table>
</template>

<script>
import axios from "axios";
export default {
  props: {
    county_id: Number,
  },
  data() {
    return {
      datas: [],
    };
  },
  computed: {
    filteredCities() {
      return this.datas.filter((city) => city.county_id === this.county_id);
    },
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      axios
        .get(`http://127.0.0.1:8000/api/citytable`)
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
