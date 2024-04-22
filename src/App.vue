<script setup lang="ts">
import { ref } from 'vue';

const textIndex = ref<0 | 1 | 2>(0);

const listOfTitles: string[] = [
  'Atomic Code',
  'Qader Kamal',
  'Timmy terminal',
];

const changeText = function () {
  textIndex.value++;
  if (textIndex.value == 3) {
    textIndex.value = 0;
  }
};
</script>

<template>
  <div class="bg-black">
    <h1
      class="h-[100vh] text-center flex items-center justify-center text-6xl bg-gradient-to-tr from-green-500 to-teal-700 bg-clip-text text-transparent relative font-mono font-extrabold"
    >
      <span @mouseover="changeText">{{
        listOfTitles[textIndex]
      }}</span
      ><span class="cursor-block"></span>
    </h1>
  </div>
</template>

<style>
.cursor-block {
  display: inline-block;
  width: 0.55em;
  height: 1em;
  background-color: rgb(10, 127, 63);
  animation: blink 0.7s steps(1, start) infinite;
}

@keyframes blink {
  50% {
    opacity: 0;
  }
}
</style>
