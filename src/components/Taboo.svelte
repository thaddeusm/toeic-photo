<script>
	import Countdown from './Countdown.svelte';
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let photo;
	export let tabooData;

	console.log(tabooData);

	let stage = 'describe';

	function endTask() {
		console.log('end')

		stage = 'win'
	}

	function reset() {
		dispatch('change-mode', 'start');
	}
</script>

<style>
header {
	position: fixed;
	top: 10px;
	left: 10px;
	padding: 10px;
	background: var(--black);
	text-align: center;
}

aside {
	position: fixed;
	top: 20px;
	right: 12px;
	padding: 10px;
}

h1 {
	color: var(--light-gray);
}

h4 {
	color: var(--light-gray);
}

ul {
	margin-top: 20px;
	display: grid;
}

li {
	margin: 10px 0;
}

button {
	color: var(--white);
	background: var(--black);
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
}

footer {
	position: fixed;
	bottom: 10px;
	right: 10px;
	display: inline-block;
	padding: 10px;
	background: var(--black);
}

.yellow {
	color: var(--yellow);
}
</style>

<div>
	<header>
		{#if stage == 'describe'}
			<h1 class="yellow">{tabooData.term}</h1>
			<ul>
				{#each tabooData["relatedWords"] as word}
					<li><h4>{word}</h4></li>
				{/each}
			</ul>
		{:else}
			<h1 class="yellow">{tabooData.term}</h1>	
		{/if}
	</header>
	<aside>
		{#if stage == 'describe'}
			<button on:click="{endTask}">done</button>
		{:else}
			<button on:click="{reset}">back</button>
		{/if}
	</aside>
	<main>
		<img src="{photo.src.medium}" alt="{`Photo by ${photo.photographer}`}">
	</main>
	<footer>
		{#if stage == 'describe'}
			<Countdown seconds="{120}" on:stopped={endTask} />
		{/if}
	</footer>
</div>