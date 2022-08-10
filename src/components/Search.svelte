<script>
    import { goto } from '$app/navigation';
    import { fly } from 'svelte/transition';

    let inputVal = "";
    let active = false;

    const submitSearch = () => {
        let href=`/search/${inputVal}`
        goto(href);
    };
</script>

<form class="search" on:submit|preventDefault={submitSearch}>
    {#if !active}
        <label in:fly={{ y: -10, duration: 500 }} out:fly={{ y: -10, duration: 500 }} for='search_movie'>Search Movie</label>
    {/if}
    <input 
        on:focus={() => active = true} 
        on:blur={() => inputVal === "" ? active = false : active = true}
        type="text" 
        name="search_movie" 
        bind:value={inputVal}
        class={active ? 'selected' : ''}
    />
    {#if inputVal !== ""}
        <button in:fly={{ duration: 500 }} out:fly={{ duration: 500 }} >Search</button>
    {/if}
</form>

<style lang="scss">

    .search {
        position: relative;
        width: 30%;
        margin: 1rem;

        label {
            font-family: "Poppins", sans-serif;
            position: absolute;
            font-size: .8rem;
            top: 50%;
            left: 0;
            transform: translate(0, -50%);
            pointer-events: none;
            color: #fff;
            padding: 0 1rem;
        }

        input {
            width: 99%;
            border: none;
            font-size: 1rem;
            font-family: "Poppins", sans-serif;
            outline: none;
            color: rgb(255, 255, 255);
            padding: 1rem .1rem;
            transition: background .75s ease-out;
            font-weight: bold;
            background: rgb(63, 63, 63);
            border-radius: 10px;
        }

        .selected {
            background-color: rgb(50, 50, 50);
        }

        button {
            font-size: .7rem;
            padding: 0 1rem;
            background: rgb(96,110,201);
            color: #fff;
            font-weight: bold;
            position: absolute;
            bottom: 50%;
            right: 0;
            transform: translate(0, 50%);
            height: 100%;
            border-top-right-radius: 10px;
            border-bottom-right-radius: 10px;
            border: none;
            cursor: pointer;
        }
    }

</style>