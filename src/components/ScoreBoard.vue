<script setup lang="ts">
import { defineProps } from "vue";

defineProps({
  score: Number,
});
</script>

<template>
  <article
    class="flex justify-between items-center border-[3px] [border-color:rgba(255,255,255,0.2892)] w-full py-[12px] pr-[12px] md:max-w-[700px] md:rounded-lg md:py-[18px] md:pr-[18px] ]"
  >
    <div
      class="pl-[23px] text-[21px] leading-4 text-[#FFFFFF] font-bold md:text-[40px] md:leading-[32px] md:font-extrabold md:pl-[32px]"
    >
      <p>ROCK</p>
      <p>PAPER</p>
      <p>SCISSORS</p>
    </div>
    <div
      class="w-[80px] h-[72px] bg-[linear-gradient(to_bottom,_#F3F3F3,_#FFFFFF)] rounded flex flex-col items-center justify-center py-[22px] md:h-[114px] md:w-[150px]"
    >
      <p class="text-[10px] font-semibold text-[#2A45C2] md:text-[16px]">
        SCORE
      </p>
      <h3
        class="text-[40px] leading-[40px] font-bold text-[#565468] md:text-[64px] md:leading-[64px]"
      >
        {{ score }}
      </h3>
    </div>
  </article>
</template>
