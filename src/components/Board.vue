<script setup>
import PaperIcon from "./PaperIcons.vue";
import RockIcon from "./rockIcon.vue";
import ScissorsIcon from "./ScissorsIcon.vue";
import { ref } from "vue";

const userSelection = ref(null);
const houseSelection = ref(null);
const showHousePick = ref(false);
const winner = ref(null);
const choices = ["rock", "paper", "scissors"];
const getRandomChoice = () => {
  const randomIndex = Math.floor(Math.random() * choices.length);
  return choices[randomIndex];
};

const handleUserSelection = (choice) => {
  userSelection.value = choice;
  console.log("User chose:", choice);
  showHousePick.value = false;

  setTimeout(() => {
    houseSelection.value = getRandomChoice();
    console.log("User chose:", houseSelection.value);
    showHousePick.value = true;
  }, 1000); // 1 second delay
};
</script>

<template>
  <article class="flex justify-center items-center w-full h-[282px]">
    <section
      class="relative w-full flex justify-center items-center"
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
