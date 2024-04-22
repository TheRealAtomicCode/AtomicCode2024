<script setup lang="ts">
	import { ref } from 'vue';
	import Header from './components/Header.vue';
	import Blob from './components/Blob.vue';

	const chooseRandomLetter = () => {
		return letters[Math.floor(Math.random() * letters.length)];
	};

	const letters = '0001';
	const text = ref<string>('v');

	for (let i = 0; i < 10000; i++) {
		text.value += chooseRandomLetter();
	}

	// give me a function that chooses a randm letter from the list
	const changeText = () => {
		text.value = '';

		for (let i = 0; i < 5000; i++) {
			text.value += chooseRandomLetter();
		}
	};

	changeText();
</script>

<template>
	<div @mousemove="changeText">
		<Blob />
		<p
			class="text-gray-900 font-mono absolute z-10 h-auto max-h-full w-[100%] overflow-y-auto whitespace-pre-wrap break-all opacity-30"
		>
			{{ text }}
		</p>
		<Header />
	</div>
</template>
