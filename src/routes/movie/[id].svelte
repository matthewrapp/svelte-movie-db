<script context="module">

    export async function load({fetch, params}) {
        const { VITE_MOVIEDB_AKI_KEY } = import.meta.env;

        const res = await fetch(`https://api.themoviedb.org/3/movie/${params.id}?api_key=${VITE_MOVIEDB_AKI_KEY}&language=en-US&page=1`);
        const movieDetails = await res.json();
        if (res.ok) {
            return { props: { movieDetails } }
        } 
    }

</script>

<script>
    import { fly } from 'svelte/transition';
    export let movieDetails;
</script>

<div class="movie-details" in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
    <div class="img-container">
        <img src={`https://image.tmdb.org/t/p/original/${movieDetails.backdrop_path}`} alt={movieDetails.title} />
    </div>
    <div class="txt-container">
        <h1>{movieDetails.title}</h1>
        <p class="overview">{movieDetails.overview}</p>
        <p>
            <span>Release Date:</span> {movieDetails.release_date} <br />
            <span>Budget:</span> {movieDetails.budget} <br />
            <span>Rating:</span> {movieDetails.vote_average} <br />
            <span>Runtime:</span> {movieDetails.runtime} <br />
        </p>
    </div>
</div>

<style lang="scss">

    .movie-details {
        margin: 2rem 20%;

        .img-container {
            width: 100%;

            img {
                width: 100%;
                border-radius: 1rem;
            }
        }

        .txt-container {

            h1 {
                padding: 1rem 0 2rem;
            }

            p {
                padding: 1rem 0;
            }

            p.overview {

            }

            p:last-child {

                span {
                    font-weight: bold;
                }
            }
        }
    }

</style>