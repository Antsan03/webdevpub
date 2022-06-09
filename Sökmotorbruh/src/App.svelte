<script>
    import Spinner from "./Spinner.svelte";
    import Results from "./Results.svelte";
    import Search from "./Search.svelte";
    import { promise } from "./Stores.js";
</script>

<main class:search={$promise != undefined}>
    <h1>You Might Die In Mere Seconds</h1>

    <Search/>

    {#await $promise}
        <Spinner />
    {:then result}
        <Results json={result} />
    {:catch error}
        <p style="color: red">{error.message}</p>
    {/await}

</main>

<style>

    :global(body) {
        background-image: url("https://upload.wikimedia.org/wikipedia/commons/2/21/A_lonely_forest_way.jpg");
        background-repeat: no-repeat, repeat;
        background-position: center;
        background-size: cover;
        overflow: hidden;
    }
    main {
        height: 100vh;
        width: 100vw;
        display: flex;
        justify-content: start;
        align-items: center;
        flex-direction: column;
        gap: 10px;
        padding-top: 13%;
        padding-left: 10%;
        padding-right: 10%;
        padding-bottom: 5%;
        box-sizing: border-box;
    }

    @keyframes moveUp {
        0%   {top:0px;}
        100%  {top:-180px;}
        }

    h1{
        color: black;
        font-family: 'Oswald', sans-serif;
        text-align: center;
    }

    main.search{
        position: relative;
        animation-name: moveUp;
        animation-duration: 1s;
        animation-fill-mode: forwards;  
    }

	@media (max-width: 600px) {
		main{
            padding-left: 0cm;
            padding-right: 0cm;
        }
        
	}
</style>