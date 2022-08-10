<script context="module">

    export async function load({fetch}) {
        const { VITE_MOVIEDB_AKI_KEY } = import.meta.env;

        const res = await fetch(`https://api.themoviedb.org/3/movie/popular?api_key=${VITE_MOVIEDB_AKI_KEY}&language=en-US&page=1`);
        const data = await res.json();
        if (res.ok) {
            return { props: { popular: data.results } }
        } 
    }

</script>

<script>
    import { fly } from 'svelte/transition';
    import Movies from '../components/Movies.svelte';
    import Search from '../components/Search.svelte';

    // to access props
    // option 1
    // export let popular;
    // option 2
    let { popular } = $$props;
</script>

<section in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
    <Search />
    <Movies movies={popular} />
</section>
