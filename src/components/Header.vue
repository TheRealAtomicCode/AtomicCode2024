<script setup lang="ts">
	import { ref } from 'vue';

	const textIndex = ref<0 | 1 | 2 | 3 | 4>(0);

	const letters =
		'ABCDEFGHIJKLMNOPQRSTUVWXYZ 1234567890!@#$%^&*()_-卡德尔卡迈勒';

	const listOfTitles: string[] = [
		'ATOMIC CODE',
		'QADER KAMAL',
		'ATOMIC CODE',
		'  عبدالقادر',
		'原子密码       ',
	];

	const name = ref<string>('ATOMIC CODE');

	const changeText = () => {
		let iterations = 1 / 4;

		textIndex.value += 1;
		if (textIndex.value === 5) {
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
	<div class="bg-gray-900">
		<h1
			:dir="textIndex !== 3 ? 'ltr' : 'rtl'"
			:class="
				textIndex === 0 || textIndex === 1 || textIndex === 4
					? 'eng'
					: textIndex === 3
					? 'ar'
					: 'bar'
			"
			class="h-[100vh] text-center flex items-center justify-center text-7xl bg-gradient-to-tr from-white to-white bg-clip-text text-transparent relative z-20"
		>
			<span @mouseover="changeText">{{ name }}</span
			><span v-if="textIndex !== 2" class="cursor-block"></span>
		</h1>
	</div>
</template>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@200..1000&family=Jersey+10&family=Jersey+25&display=swap');
	@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@200..1000&family=Jersey+10&family=Jersey+25&family=Libre+Barcode+39+Extended+Text&display=swap');
	@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@200..1000&family=Jersey+10&family=Jersey+25&family=Libre+Barcode+39+Extended+Text&family=Roboto+Flex:opsz,wght@8..144,100..1000&display=swap');
	.cursor-block {
		display: inline-block;
		width: 0.55em;
		height: 1em;
		background-color: rgb(255, 255, 255);
		animation: blink 0.7s steps(1, start) infinite;
	}

	@keyframes blink {
		50% {
			opacity: 0;
		}
	}

	.ar {
		font-family: 'Cairo', sans-serif;
		font-optical-sizing: auto;
		font-weight: 700;
	}

	.bar {
		font-family: 'Libre Barcode 39 Extended Text', system-ui;
		font-weight: 400;
		font-style: normal;
	}

	.eng {
		font-family: 'Roboto Flex', sans-serif;
		font-optical-sizing: auto;
	}
</style>
