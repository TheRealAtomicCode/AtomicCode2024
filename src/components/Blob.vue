<template>
	<div
		id="blob"
		class="absolute bg-gradient-to-r blur-3xl from-sky-400 to-teal-400 w-96 h-72 rounded-full animate-rotate-custom"
		:style="{
			transform: `translate(${position.x - 120}px, ${
				position.y - 190
			}px) scale(1.2)`,
			transition: 'transform 0.8s ease-out',
		}"
	></div>
</template>

<script setup lang="ts">
	import { ref, onMounted, onUnmounted } from 'vue';

	interface Position {
		x: number;
		y: number;
	}

	const position = ref<Position>({ x: 180, y: 290 });

	const handleMouseMove = (event: MouseEvent) => {
		position.value = { x: event.clientX, y: event.pageY };
	};

	const handleScroll = () => {
		position.value = { ...position.value, y: window.pageYOffset + 290 };
	};

	onMounted(() => {
		window.addEventListener('mousemove', handleMouseMove);
		window.addEventListener('scroll', handleScroll);
	});

	onUnmounted(() => {
		window.removeEventListener('mousemove', handleMouseMove);
	});
</script>
