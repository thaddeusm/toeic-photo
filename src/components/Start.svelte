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
}
</style>

<main>
	<section class="top">
		<button on:click="{selectTest}" disabled="{!loaded}">Test</button>
	</section>
	<img src="./logo.svg" alt="logo">
	<section class="bottom">
		<button on:click="{selectTaboo}" disabled="{!loaded}">Taboo</button>		
	</section>
</main>

