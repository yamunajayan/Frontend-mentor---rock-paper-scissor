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
    // Delay the winner determination by 1 second
    setTimeout(() => {
      determineWinner();
    }, 1000);
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
      class="relative w-full flex justify-center items-center h-[282px] md:h=[436px]"
      v-if="userSelection === null"
    >
      <div class="absolute z-0 px-[73px]">
        <img
          src="/bg-triangle.svg"
          alt="background triangle"
          class="w-full h-[188px] md:w-[254px] md:h-[288px]"
        />
      </div>
      <div
        class="absolute h-[288px] md:h-[430px] w-full z-10 flex flex-col justify-between items-center"
      >
        <div
          class="flex justify-between items-center w-full max-w-sm md:max-w-[476px]"
        >
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
      :class="[
        'flex justify-between items-center w-full h-[182px] md:h-[300px]',
        winner ? 'md:max-w-[800px]' : 'md:max-w-[600px]',
      ]"
    >
      <div class="flex flex-col justify-between items-center h-full">
        <p class="hidden md:block">YOU PICKED</p>
        <PaperIcon v-if="userSelection === 'paper'" />
        <RockIcon v-else-if="userSelection === 'rock'" />
        <ScissorsIcon v-else-if="userSelection === 'scissors'" />
        <p class="md:hidden">YOU PICKED</p>
      </div>
      <div class="flex flex-col justify-between items-center h-full">
        <p class="hidden md:block">THE HOUSE PICKED</p>
        <PaperIcon v-if="showHousePick && houseSelection === 'paper'" />
        <RockIcon v-else-if="showHousePick && houseSelection === 'rock'" />
        <ScissorsIcon
          v-else-if="showHousePick && houseSelection === 'scissors'"
        />
        <div v-else class="w-[130px] h-[133px]"></div>
        <p class="md:hidden">THE HOUSE PICKED</p>
      </div>
    </section>
  </article>
</template>
