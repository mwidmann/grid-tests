<template>
  <div id="app"><ItemsList /></div>
</template>

<script>
import ItemsList from "./components/ItemsList";

export default {
  name: "App",
  components: {
    ItemsList
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
