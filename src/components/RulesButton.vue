<script setup>
import { ref } from "vue";

const showRules = ref(false);
const handleRuleClick = () => {
  showRules.value = !showRules.value;
  console.log("clicked");
};
</script>
<template>
  <div
    class="relative h-[40px] w-[128px] rounded-lg border-[1px] border-[#FFFFFF] flex justify-center items-center cursor-pointer mb-4"
    @click="handleRuleClick"
  >
    <p class="text-[16px]">RULES</p>
  </div>
  <div
    v-if="showRules"
    class="z-20 fixed w-full h-full bg-white top-0 flex flex-col items-center justify-around"
  >
    <h1 class="text-[32px] font-bold text-[#3B4262]">RULES</h1>
    <img src="/image-rules.svg" alt="rules icon" class="w-[305px] h-[271px]" />
    <button>
      <img
        src="/icon-close.svg"
        alt="close icon"
        class=""
        @click="handleRuleClick"
      />
    </button>
  </div>
</template>
