<script setup>
import PaperIcon from "./PaperIcons.vue";
import RockIcon from "./RockIcon.vue";
import ScissorsIcon from "./ScissorsIcon.vue";
import { ref, defineEmits, defineExpose } from "vue";

const emit = defineEmits();

const userSelection = ref(null);
const houseSelection = ref(null);
const showHousePick = ref(false);
const winner = ref(null);
const choices = ["rock", "paper", "scissors"];
const getRandomChoice = () => {
  const randomIndex = Math.floor(Math.random() * choices.length);
  return choices[randomIndex];
};

const resetGame = () => {
  userSelection.value = null;
  houseSelection.value = null;
  showHousePick.value = false;
  winner.value = null;
  console.log("Board reset");
};

defineExpose({
  resetGame,
});

const handleUserSelection = (choice) => {
  userSelection.value = choice;
  console.log("User chose:", choice);
  showHousePick.value = false;

  setTimeout(() => {
    houseSelection.value = getRandomChoice();
    console.log("User chose:", houseSelection.value);
    showHousePick.value = true;
    determineWinner();
  }, 1000); // 1 second delay

  // 2 seconds delay
};

const determineWinner = () => {
  if (userSelection.value === houseSelection.value) {
    winner.value = "draw"; // No winner if it's a tie
  } else if (
    (userSelection.value === "rock" && houseSelection.value === "scissors") ||
    (userSelection.value === "scissors" && houseSelection.value === "paper") ||
    (userSelection.value === "paper" && houseSelection.value === "rock")
  ) {
    winner.value = "user"; // User wins
  } else {
    winner.value = "house"; // House wins
  }

  emit("updateWinner", winner.value); // Emit 'user' or 'house' to parent
};
</script>

<template>
  <article class="flex justify-center items-center w-full">
    <section
      class="relative w-full flex justify-center items-center h-[282px]"
      v-if="userSelection === null"
    >
      <div class="absolute z-0 px-[73px]">
        <img
          src="/bg-triangle.svg"
          alt="background triangle"
          class="w-full h-[188px]"
        />
      </div>
      <div
        class="absolute h-[288px] w-full z-10 flex flex-col justify-between items-center"
      >
        <div class="flex justify-between items-center w-full max-w-sm">
          <div @click="handleUserSelection('paper')" class="cursor-pointer">
            <PaperIcon />
          </div>
          <div @click="handleUserSelection('scissors')" class="cursor-pointer">
            <ScissorsIcon />
          </div>
        </div>
        <div>
          <div @click="handleUserSelection('rock')" class="cursor-pointer">
            <RockIcon />
          </div>
        </div>
      </div>
    </section>
    <section
      v-else
      class="flex justify-between items-center w-full max-w-sm h-[182px]"
    >
      <div class="flex flex-col justify-between items-center h-full">
        <PaperIcon v-if="userSelection === 'paper'" />
        <RockIcon v-else-if="userSelection === 'rock'" />
        <ScissorsIcon v-else-if="userSelection === 'scissors'" />
        <p>YOU PICKED</p>
      </div>
      <div class="flex flex-col justify-between items-center h-full">
        <PaperIcon v-if="showHousePick && houseSelection === 'paper'" />
        <RockIcon v-else-if="showHousePick && houseSelection === 'rock'" />
        <ScissorsIcon
          v-else-if="showHousePick && houseSelection === 'scissors'"
        />
        <div v-else class="w-[130px] h-[133px]"></div>
        <p>THE HOUSE PICKED</p>
      </div>
    </section>
  </article>
</template>
