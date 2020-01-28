<script>
	export let name;
	import Header from './header.svelte';
	import SearchBox from './searchBox.svelte';
	import SearchButton from './SearchButton.svelte';
	import ImageGallery from './ImageGallery/Image.svelte';

	let selected = null;
	function handleClick() {
		selected = true
	}
</script>

<main>
	<Header/>
	<SearchBox/>
	<!-- <SearchButton/> -->
	<!-- <h1>Hello {name}!</h1> -->
	<ImageGallery/>
	<!-- <p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p> -->
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		/* max-width: 240px; */
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>