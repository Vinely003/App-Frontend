<template>
  <form class="m-4" action="">
    <div class="input-group mx-auto" style="width: 15%">
      <span class="input-group-text" id="inputGroup-sizing-default"
        >Új város</span
      >
      <input
        type="text"
        class="form-control"
        aria-label="Sizing example input"
        aria-describedby="inputGroup-sizing-default"
        v-model="cityName"
      />
      <button
        class="btn btn-outline-secondary"
        type="button"
        id="button-addon2"
        @click="newCity"
      >
        Megerősítés
      </button>
    </div>
  </form>
</template>

<script>
import axios from "axios";

export default {
  props: {
    county_id: Number,
  },
  data() {
    return {
      cityName: "",
      datas: [],
    };
  },
  afterUpdated() {
    this.fetchData();
    this.cityName = "";
  },
  methods: {
    async newCity() {
      try {
        const response = await axios.post("http://127.0.0.1:8000/api/cities", {
          name: this.cityName,
          county_id: this.county_id,
        });
        this.datas.push(response.data);
      } catch (error) {
        console.error("Hiba történt a város küldésekor:", error);
      }
    },
  },
};
</script>
