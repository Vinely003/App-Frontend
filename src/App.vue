<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Hello World!" />
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld,
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
