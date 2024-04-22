<script setup lang="ts">
import { ref } from 'vue';

const textIndex = ref<0 | 1 | 2>(0);

const letters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ 1234567890!@#$%^&*()_-';

const listOfTitles: string[] = ['ATOMIC CODE', 'QADER KAMAL'];

const name = ref<string>('ATOMIC CODE');

const changeText = () => {
  let iterations = 1 / 3;

  textIndex.value += 1;
  if (textIndex.value === 2) {
    textIndex.value = 0;
  }

  const interval = setInterval(() => {
    const word = name.value
      .split('')
      .map((letter, index) => {
        if (index < iterations) {
          return listOfTitles[textIndex.value][index];
        }

        return letters[Math.floor(Math.random() * 48)];
      })
      .join('');
    name.value = word;

    if (iterations >= listOfTitles[textIndex.value].length)
      clearInterval(interval);

    iterations += 1;
  }, 40);
};
</script>

<template>
  <div class="bg-black">
    <h1
      class="h-[100vh] text-center flex items-center justify-center text-6xl bg-gradient-to-tr from-green-500 to-teal-700 bg-clip-text text-transparent relative font-mono font-extrabold"
    >
      <span @mouseover="changeText">{{ name }}</span
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
