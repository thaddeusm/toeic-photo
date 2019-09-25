<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let loaded;

	function selectTest(event) {
		dispatch('change-mode', 'test');
	}

	function selectTaboo(event) {
		dispatch('change-mode', 'taboo');
	}
</script>

<style>
@keyframes flip {
	from {transform: rotateY(0);}
	to {transform: rotateY(160deg);}
}

@keyframes fade {
	from {opacity: 0;}
	to {opacity: 1;}
}

@media screen and (max-width: 450px) {
	main {
		height: 100%;
		display: grid;
		grid-template-rows: .5fr 1fr 1fr 1fr .5fr;
		grid-template-areas: 
			"."
			"top"
			"logo"
			"bottom"
			".";
		text-align: center;
		align-items: center;
		background: var(--black);
	}
}

@media screen and (min-width: 451px) {
	main {
		height: 100%;
		display: grid;
		grid-template-columns: 25vw 1fr 25vw;
		grid-template-areas: "top logo bottom";
		text-align: center;
		align-items: center;
		background: var(--black);
	}
}

.loading {
	animation-name: flip;
	animation-duration: infinite;
	animation-delay: 200ms;
	animation-timing-function: ease-in;
	animation-duration: .7s;
}

.top {
	grid-area: top;
}

.bottom {
	grid-area: bottom;
}

img {
	width: 150px;
	display: block;
	margin: 0 auto;
	grid-area: logo;
}

button {
	padding: 1em 2em;
	background: var(--yellow);
	border-radius: .5em;
	animation-name: fade;
	animation-duration: 1s;
	animation-timing-function: ease-in;
}
</style>

<main>
	<section class="top">
		{#if loaded}
			<button on:click="{selectTest}">Test</button>
		{/if}
	</section>
	<img src="./logo.svg" alt="logo" class="loading">
	<section class="bottom">
		{#if loaded}
			<button on:click="{selectTaboo}">Taboo</button>
		{/if}	
	</section>
</main>

