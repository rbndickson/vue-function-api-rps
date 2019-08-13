<template>
  <div id="app">
    <main>
      <Game />
    </main>
  </div>
</template>

<script>
import Game from "./components/Game.vue";

export default {
  name: "app",
  components: {
    Game
  }
};
</script>

<style>
main {
  font-family: "Courier New", Courier, monospace;
  min-width: 400px;
  max-width: 800px;
  margin: auto;
}
</style>
