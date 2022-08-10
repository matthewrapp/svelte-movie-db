<script context="module">

    export async function load({fetch, params}) {
        const { VITE_MOVIEDB_AKI_KEY } = import.meta.env;

        const res = await fetch(`https://api.themoviedb.org/3/search/movie?api_key=${VITE_MOVIEDB_AKI_KEY}&language=en-US&query=${params.query}&page=1&include_adult=false`);
        const searchResults = await res.json();
        if (res.ok) {
            return { props: { movieResults: searchResults.results, searchQuery: params.query } }
        } 
    }

</script>

<script>
    import MovieCard from "../../components/MovieCard.svelte";
    export let movieResults, searchQuery;
</script>

<div class="searched-movies">
    <h3>Search results for {searchQuery}</h3>
    <div class="movies-container">
        {#each movieResults as movie}
            <MovieCard {movie} />
        {/each}
    </div>
</div>

<style lang="scss">
    .searched-movies {

        h3 {
            font-family: "Poppins", sans-serif;
            padding: 0 1rem;
        }
        
        .movies-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            column-gap: 1rem;
            row-gap: 2rem;
        }
    }
</style>