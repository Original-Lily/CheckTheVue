<template>
  <div id="app">
    <Weather />
  </div>
</template>

<script>
import Weather from "@/components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    Weather,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #000000;
  margin-top: 60px;
}
</style>
