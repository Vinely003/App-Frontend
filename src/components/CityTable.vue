<template>
  <table class="table table-striped mx-auto" style="width: 45%">
    <tbody>
      <tr v-for="data in filteredCities" :key="data.id">
        <th scope="row">
          <div @click="showButtons">
            {{ data.name }}
          </div>
          <div v-if="buttons">
            <button
              @click="updateCity"
              :update="data.id"
              class="btn btn-primary"
            >
              Update
            </button>
            <button @click="cancel" :cancel="data.id" class="btn btn-secondary">
              Cancel
            </button>
            <button
              @click="deleteCity"
              :delete="data.id"
              class="btn btn-danger"
            >
              Delete
            </button>
          </div>
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
      delete: null,
      buttons: false,
    };
  },
  computed: {
    filteredCities() {
      return this.datas.filter((city) => city.county_id === this.county_id);
    },
  },
  watch: {
    delete(newdelete) {
      console.log(newdelete);
    },
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    showButtons() {
      this.buttons = !this.buttons;
    },
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
    async deleteCity() {
      try {
        await axios.delete("http://127.0.0.1:8000/api/destroy", {
          id: this.delete,
        });
      } catch (error) {
        console.error("Hiba történt a város küldésekor:", error);
      }
    },
  },
};
</script>
