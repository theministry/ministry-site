<script>
    import data from '../data/data.json'

    import Window from './Window.svelte'
    import FolderIcon from './FolderIcon.svelte'

    export let title;
    export let content;
    export let id;
</script>

<style>
    div.main {
        margin-top: 22px;
        border-radius: 4px;
        border: 2px solid black;
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        overflow-y: scroll;
    }

    div.trash {
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: row;
        align-items: center;
        vertical-align: middle;
    }

    div.trash p {
        margin: auto;
        text-align: center;
    }
</style>

<Window
    id={id}
    title={title}
    controls={true}

    on:open
    on:close
    on:focus
>
    <div class="main">
        {#if content === "studio"}

            <FolderIcon title={data.studio[1].name} type="about" content={data.studio[1]} on:open />

        {:else if content === "projects"}
            {#each data.projects as item }
                <FolderIcon title={item.name} type="project" content={item} on:open />
            {/each}
        {:else if content === "trash"}
        <div class="trash"><p>The trash is empty.</p></div>
        {:else}
        <p>empty folder</p>
        {/if}
    </div>
</Window>