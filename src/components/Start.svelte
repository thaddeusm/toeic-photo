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
	to {transform: rotateY(180deg);}
}

@keyframes fade {
	from {opacity: 0;}
	to {opacity: 1;}
}

@media screen and (max-width: 450px) {
	main {
		height: 100%;
		display: grid;
		grid-template-rows: 15% 20% 30% 20% 15%;
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
		grid-template-columns: 25% 50% 25%;
		grid-template-areas: "top logo bottom";
		text-align: center;
		align-items: center;
		background: var(--black);
	}
}

.loading {
	animation-name: flip;
	animation-iteration-count: infinite;
	animation-timing-function: ease-in-out;
	animation-duration: 1.3s;
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
	animation-timing-function: ease-in-out;
}
</style>

<main>
	<section class="top">
		{#if loaded}
			<button on:click="{selectTest}">Test</button>
		{/if}
	</section>
	<img src="./logo.svg" alt="logo" class:loading="{!loaded}">
	<section class="bottom">
		{#if loaded}
			<button on:click="{selectTaboo}">Taboo</button>
		{/if}	
	</section>
</main>

