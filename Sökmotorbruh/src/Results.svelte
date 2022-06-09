<script>
    export let json;
    import { fly, fade, slide, draw } from "svelte/transition";
</script>

{#if json && "data" in json && "items" in json.data && json.data.items.length > 0}
    <div id = "item-holder">
        {#each json.data.items as item}
            <div onclick="location.href='{item.url}';" style="cursor: pointer;" id = "item">
                <p in:fade id="url">{item.url}</p>
                <p in:fade id="name">{item.name}</p>
                <p in:fade>{item.published_at}</p>
                <p in:fade>{item.type}</p>
            </div>
        {/each}
    </div>
{:else if json}
    <div>
        <p in:fade id="youDied">You Died</p>
    </div>
{/if}

<style>
    #item-holder {
        display: flex;
        justify-content: start;
        align-items: center;
        flex-direction: column;
        overflow-y: scroll;
        box-sizing: border-box;
        padding-left: 10%;
        padding-right: 10%;
        max-width: 70%;
        row-gap: 20px;
    }
    #item {
        border-radius: 25px;
        background-color: rgb(255, 255, 255);
        border: 2px solid rgb(255, 255, 255);
        padding: 20px;
        width: 100%;
        box-sizing: border-box;
        word-wrap: break-word;
    }
    #name:hover {
        text-decoration: underline;
    }
    #url {
        font-size: x-small;
    }
    #name {
        font-size: x-large;
        margin-top: 5px;
        margin-bottom: 5px;
        color: blue;
    }
    #youDied {
        font-family: Impact, Haettenschweiler, 'Arial Narrow Bold', sans-serif;
        font-size: larger;
    }

    p{
        color: rgb(0, 0, 0);
    }

    /** https://onaircode.com/html-css-custom-scrollbar-examples/ */
    ::-webkit-scrollbar {
        width: 15px;
        height: 15px;
    }
    ::-webkit-scrollbar-track {
        border-radius: 10px;
        background-color: rgba(255, 255, 255, 0.1);
    }
    ::-webkit-scrollbar-thumb {
        background-image: linear-gradient(45deg, #00aeff, #a68eff);
        border-radius: 10px;
        -webkit-box-shadow: rgba(0, 0, 0, 0.12) 0 3px 13px 1px;
        box-shadow: 0 3px 13px 1px rgba(0, 0, 0, 0.12);
    }
    @media (max-width: 600px) {
		#item-holder{
            padding-left: 0cm;
            padding-right: 0cm;
        }
        #item{
            padding: 5px;
        }
        
	}
</style>