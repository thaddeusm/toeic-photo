<script>
	import Countdown from './Countdown.svelte';
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let photo;

	let stage = 'prepare';

	let pauseCountdown = true;

	function startCountdown() {
		pauseCountdown = false;
	}

	function startTask() {
		stage = 'describe'
	}

	function endTask() {
		dispatch('change-mode', 'start');
	}
</script>

<style>
header {
	position: fixed;
	top: 10px;
	left: 10px;
	display: inline-block;
	padding: 0 10px;
	background: var(--black);
}

h1 {
	color: var(--light-gray);
}

main {
	display: grid;
	align-items: center;
	justify-content: center;
	text-align: center;
	height: 100vh;
}

img {
	display: block;
	max-width: 100vw;
}

footer {
	position: fixed;
	bottom: 10px;
	right: 10px;
	display: inline-block;
	padding: 0 10px;
	background: var(--black);
}
</style>

<div>
	<header>
		{#if stage == 'prepare'}
			<h1>Prepare</h1>
		{:else}
			<h1>Describe</h1>
		{/if}
	</header>
	<main>
		<img src="{photo.src.large}" alt="{`Photo by ${photo.photographer}`}" on:error="{endTask}" on:load="{startCountdown}">
	</main>
	<footer>
		{#if stage == 'prepare'}
			<Countdown seconds="{30}" on:stopped={startTask} {pauseCountdown} />
		{:else}
			<Countdown seconds="{45}" on:stopped={endTask} />
		{/if}
	</footer>
</div>
