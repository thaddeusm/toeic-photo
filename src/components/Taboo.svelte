<script>
	import Countdown from './Countdown.svelte';
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let photo;
	export let tabooData;

	let stage = 'describe';

	let pauseCountdown = false;

	function endTask() {
		stage = 'win';
		pauseCountdown = true;
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
	top: 10px;
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
	list-style: none;
}

li {
	margin: 10px 0;
	text-indent: none;
}

button {
	color: var(--white);
	background: var(--black);
	padding: 10px;
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
		<img src="{photo.src.large}" alt="{`Photo by ${photo.photographer}`}">
	</main>
    <footer>
        <Countdown seconds="{120}" on:stopped={endTask} {pauseCountdown} />
    </footer>
</div>
