<script>
	import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

	export let seconds;

	let time = seconds;

	let running;

	function countdown() {
		time--;

		if (time == 0) {
			stop();
		}
	}

	function start() {
		running = setInterval(countdown, 1000);
	}

	function stop() {
		clearInterval(running);
		dispatch('stopped');
	}

	setTimeout(function() {
		start()
	}, 2000);
</script>

<style>
h3 {
	color: var(--yellow);
}
</style>

<h3>{time}</h3>
