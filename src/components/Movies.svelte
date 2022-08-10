<script>
    import MovieCard from "./MovieCard.svelte";
    const { movies } = $$props;
</script>

<h3>POPULAR MOVIES</h3>
<div class="movies">
    {#each movies as movie}
        <MovieCard {movie} />
    {/each}
</div>

<style lang="scss">
    
    h3 {
        padding: 0 1rem;
    }

    .movies {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
        column-gap: 1rem;
        row-gap: 2rem;
    }

</style>