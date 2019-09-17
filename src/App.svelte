<script>
	import Start from './components/Start.svelte';
	import Test from './components/Test.svelte';
	import Taboo from './components/Taboo.svelte';
	import End from './components/End.svelte';
	import searchTerms from './searchTerms.json';

	let testPhotos = [];
	let testPhotoIndex;

	let tabooTopicIndex = null;
	let tabooPhotoIndex;
	let tabooPhotos = [];

	let mode = 'start';

	function chooseRandomPhoto(type) {
		if (type == 'test') {
			testPhotoIndex = Math.floor(Math.random() * testPhotos.length);
		} else {
			tabooPhotoIndex = Math.floor(Math.random() * tabooPhotos.length);
		}
	}

	function getTestPhotos() {
		let request = new XMLHttpRequest();
		request.open('GET', 'https://toeic-photo-api-git-master.thaddeusmccleary.now.sh/api/index.js');
		request.addEventListener('load', (results) => {
			let parsed = JSON.parse(results.target.response);

			testPhotos = parsed.photos.photos;

			console.log('Test photos:', testPhotos);

			chooseRandomPhoto('test');
		})
		request.send();
	}

	function getTabooPhotos() {
		let baseUrl = 'https://toeic-photo-api-git-master.thaddeusmccleary.now.sh/api/search.js?searchTerm=';

		tabooTopicIndex = Math.floor(Math.random() * searchTerms.terms.length);

		let randomSearchTerm = searchTerms.terms[tabooTopicIndex].term;

		let url = baseUrl + randomSearchTerm;

		let request = new XMLHttpRequest();
		request.open('GET', url);
		request.addEventListener('load', (results) => {
			let parsed = JSON.parse(results.target.response);

			tabooPhotos = parsed.photos.photos;

			console.log('Taboo photos:', tabooPhotos);

			chooseRandomPhoto('taboo');
		})
		request.send();
	}

	function changeMode(event) {
		console.log(event.detail);
		mode = event.detail;

		if (mode == 'start') {
			getTestPhotos();
	                getTabooPhotos();
		}
	}

	getTestPhotos();
	getTabooPhotos();
</script>

{#if mode == 'start'}
	<Start loaded="{testPhotos.length > 0 && tabooPhotos.length > 0}" on:change-mode={changeMode} />
{:else if mode == 'test'}
	<Test photo={testPhotos[testPhotoIndex]} on:change-mode={changeMode} />
{:else if mode == 'taboo'}
	<Taboo photo={tabooPhotos[tabooPhotoIndex]} tabooData="{searchTerms.terms[tabooTopicIndex]}" on:change-mode={changeMode} />
{:else}
	<End />
{/if}
