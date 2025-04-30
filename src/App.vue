<script setup lang="ts">
import ScoreBoard from "./components/ScoreBoard.vue";
import Board from "./components/Board.vue";
import RulesButton from "./components/RulesButton.vue";
// import GameBoard from "./components/GameBoard.vue";
</script>

<template>
  <main
    class="main p-8 [font-family:'Barlow_Semi_Condensed',sans-serif] flex flex-col items-center justify-between"
  >
    <ScoreBoard />
    <Board />
    <RulesButton />
  </main>
</template>

<style>
main {
  width: 100%;
  height: 100vh;
  color: #ffffff;
}

.rules-button {
  position: absolute;
  top: 20px;
  right: 20px;
}
</style>
