<script setup lang="ts">
import { defineProps, defineEmits } from "vue";

const emit = defineEmits();

const props = defineProps<{
  gameWinner: string | null;
}>();
</script>
<template>
  <section class="flex flex-col justify-between items-center w-full h-[131px]">
    <div class="flex flex-col items-center justify-between w-full h-full">
      <h3
        class="transition-opacity duration-300 font-bold text-[56px] leading-[56px] text-center uppercase"
        :class="{ 'opacity-0': !gameWinner, 'opacity-100': gameWinner }"
      >
        {{
          props.gameWinner === "user"
            ? "YOU WIN"
            : props.gameWinner === "house"
            ? "YOU LOSE"
            : "IT'S A DRAW"
        }}
      </h3>
      <button
        class="w-[220px] h-[48px] rounded-lg bg-linear-to-b from-[#F3F3F3] to-[#FFFFFF] flex justify-center items-center text-[#3B4262] font-semibold text-[16px] leading-[16px]"
        style="letter-spacing: 2.5px"
        @click="$emit('playAgain')"
      >
        PLAY AGAIN
      </button>
    </div>
  </section>
</template>
