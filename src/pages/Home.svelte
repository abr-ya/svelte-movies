<script>
	import {onMount} from 'svelte';
	import {fetchMovies} from '../api';

	// components
	import Header from '../components/Header.svelte';
	import Hero from '../components/Hero.svelte';
	import Search from '../components/Search.svelte';
	import Grid from '../components/Grid.svelte';
	import Thumb from '../components/Thumb.svelte';
	import LoadMoreButton from '../components/LoadMoreButton.svelte';
	import Spinner from '../components/Spinner.svelte';

	// state
	let movies = {movies: []};
	let isLoading;
	let searchTerm = '';
	let error;

	const handleFetchMovies = async(loadMore, searchTerm) => {
		try {
			isLoading = true;
			error = false;
			movies = await fetchMovies(movies, loadMore, searchTerm)
			console.log(movies);
		} catch (err) {
			error = true;
		}
		isLoading = false;
	};

	onMount(async() => {
		handleFetchMovies(false, searchTerm);
	});
</script>

<Header />
<Hero />
<Search />
<Grid />
<Thumb />
<LoadMoreButton />
<Spinner />

<style>

</style>
