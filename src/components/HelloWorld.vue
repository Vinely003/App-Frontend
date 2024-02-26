<template>
  <div id="hello">
    <h1>{{ msg }}</h1>
    <p>{{ para }}</p>
  </div>
</template>

<script>
export default {
  props: {
    msg: String,
  },
  data() {
    return {
      para: "Hello World!",
    };
  },
};
</script>

<style scoped>
#hello {
  background-color: yellowgreen;
  color: purple;
}
</style>
