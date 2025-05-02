<script setup lang="ts">
import ScoreBoard from "./components/ScoreBoard.vue";
import Board from "./components/Board.vue";
import RulesButton from "./components/RulesButton.vue";
import WinnerSection from "./components/WinnerSection.vue";
import { ref } from "vue";
// import GameBoard from "./components/GameBoard.vue";

const gameWinner = ref<string | null>(null);
const boardRef = ref();

const handlePlayAgain = () => {
  gameWinner.value = null;
  console.log("Play Again clicked");
  boardRef.value?.resetGame();
  // Reset the game state here
};

const handleWinner = (winner: string | null) => {
  gameWinner.value = winner;
  if (winner === "user") {
    scoreRef.value += 1;
  } else if (winner === "house") {
    scoreRef.value -= 1;
  }

  console.log("Game Winner:", gameWinner.value);
};
const scoreRef = ref<number>(0);
</script>

<template>
  <main
    class="main p-8 [font-family:'Barlow_Semi_Condensed',sans-serif] flex flex-col items-center justify-between"
  >
    <ScoreBoard :score="scoreRef" />
    <Board @updateWinner="handleWinner" ref="boardRef" />

    <div class="h-[131px] flex items-center justify-center w-full">
      <WinnerSection
        v-if="gameWinner"
        :gameWinner="gameWinner"
        @playAgain="handlePlayAgain"
      />
    </div>

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
