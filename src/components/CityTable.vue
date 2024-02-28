<template>
  <table class="table table-striped mx-auto text-center" style="width: 45%">
    <tbody>
      <tr v-for="data in filteredCities" :key="data.id">
        <th scope="row">
          <div v-if="!data.editing" @click="editCity(data)">
            {{ data.name }}
          </div>
          <div v-else>
            <input v-model="data.newName" />
            <button @click="updateCity(data)" class="btn btn-primary">
              Update
            </button>
            <button @click="cancelEdit(data)" class="btn btn-secondary">
              Cancel
            </button>
            <button @click="deleteCity(data.id)" class="btn btn-danger">
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
    showButtons() {
      this.buttons = !this.buttons;
    },
    fetchData() {
      axios
        .get(`http://127.0.0.1:8000/api/cities`)
        .then((response) => {
          this.datas = response.data.data.map((city) => ({
            ...city,
            editing: false,
            newName: city.name,
          }));
        })
        .catch((error) => {
          console.error("Hiba történt:", error);
        });
    },
    async deleteCity(cityId) {
      try {
        await axios.delete(`http://127.0.0.1:8000/api/cities/${cityId}`);
        this.datas = this.datas.filter((city) => city.id !== cityId);
      } catch (error) {
        console.error("Hiba történt a város küldésekor:", error);
      }
    },
    editCity(city) {
      city.editing = !city.editing;
    },
    async updateCity(city) {
      try {
        await axios.put(`http://127.0.0.1:8000/api/cities/${city.id}`, {
          name: city.newName,
        });
        city.name = city.newName;
        city.editing = !city.editing;
      } catch (error) {
        console.error("Hiba történt a város frissítésekor:", error);
      }
    },
    cancelEdit(city) {
      city.editing = !city.editing;
    },
  },
};
</script>
