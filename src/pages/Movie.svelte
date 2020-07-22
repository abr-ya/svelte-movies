<script>
	import {onMount} from 'svelte';
	import {fade} from 'svelte/transition';
	import {fetchMovie} from '../api';

	// comp-s
	import Navigation from '../components/Navigation.svelte';
	import Spinner from '../components/Spinner.svelte';
	import MovieInfo from '../components/MovieInfo.svelte';
	import MovieInfoBar from '../components/MovieInfoBar.svelte';
	import Actor from '../components/Actor.svelte';
	import Grid from '../components/Grid.svelte';

	export let params;

	let isLoading;
	let error;
	let movie;

	const handleFetchMovie = async () => {
		try {
			isLoading = true;
			error = false;
			movie = await fetchMovie(params.id)
			console.log(movie); // посмотреть свойства фильма
		} catch (err) {
			error = true;
		}
		isLoading = false;
	};

	onMount(async() => {
		handleFetchMovie();
	});
</script>

{#if error}
	<p>Something went wrong...</p>
{:else if movie}
	<div transition:fade={{duration: 300}}>
		<Navigation movie={movie.title} />
		<MovieInfo {movie} />
		<MovieInfoBar />
		<Actor />
		<Grid header="Actors" />
	</div>
{/if}

{#if isLoading}
	<Spinner />
{/if}

<style>

</style>
