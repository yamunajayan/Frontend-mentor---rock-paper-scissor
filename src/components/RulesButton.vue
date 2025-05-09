<script setup>
import { ref } from "vue";

const showRules = ref(false);
const handleRuleClick = () => {
  showRules.value = !showRules.value;
  console.log("clicked");
};
</script>
<template>
  <div class="flex justify-center md:justify-end w-full">
    <div
      class="relative h-[40px] w-[128px] rounded-lg border-[1px] border-[#FFFFFF] flex justify-center items-center cursor-pointer mb-4"
      @click="handleRuleClick"
    >
      <p class="text-[16px]">RULES</p>
    </div>
  </div>
  <div
    v-if="showRules"
    class="z-20 fixed h-full w-full bg-black/50 flex items-center justify-center top-[-1px]"
  >
    <div
      class="w-full h-full md:h-[415px] md:w-[415px] bg-white top-0 flex flex-col items-center justify-around md:p-4"
    >
      <div
        class="flex justify-center md:justify-between items-center w-full px-4"
      >
        <h1 class="text-[32px] font-bold text-[#3B4262]">RULES</h1>
        <button class="hidden md:block">
          <img
            src="/icon-close.svg"
            alt="close icon"
            class=""
            @click="handleRuleClick"
          />
        </button>
      </div>
      <img
        src="/image-rules.svg"
        alt="rules icon"
        class="w-[305px] h-[271px]"
      />
      <button class="md:hidden">
        <img
          src="/icon-close.svg"
          alt="close icon"
          class=""
          @click="handleRuleClick"
        />
      </button>
    </div>
  </div>
</template>
