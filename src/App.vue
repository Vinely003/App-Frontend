<template>
  <CountiesSelect />
</template>

<script>
import CountiesSelect from "./components/CountiesSelect.vue";

export default {
  name: "App",
  components: {
    CountiesSelect,
  },
};
</script>

<style>
body {
  background-image: linear-gradient(rgb(192, 193, 255), rgb(255, 192, 213));
  background-attachment: fixed;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
}
</style>
