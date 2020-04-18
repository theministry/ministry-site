<script>
    import Window from './Window.svelte'
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    export let id
    export let title
    export let content

    let size = {
        height: (window.innerHeight - 32) * 0.8,
        width: window.innerWidth * 0.8
    }

    let pos = {
        top: (window.innerHeight - size.height) / 2 + 32,
        left: (window.innerWidth -  size.width) / 2
    }
</script>

<style>
    .content {
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: row;
        padding: 20px 0;
    }

    .left, .right {
        height: 100%;
        padding: 16px;
    }

    .left {
        width: 40%;
        padding-left: 32px;
    }

    .right {
        width: 60%;
        overflow-y: scroll;
        padding-right: 32px;
    }

    .image {
        width: 100%;
        height: 100%;
        border: 2px solid black;
        cursor: pointer;
    }

    h5 {
        margin-bottom: 4px;
    }

    a {
        display: block;
        color: #078DFF;
        font-weight: bold;
        text-decoration: none;
        font-size: 14px;
    }

    a:hover {
        color: #003DFF;
    }


</style>

<Window
    id={id}
    title={title}
    controls=true

    size={size}
    pos={pos}

    on:close
    on:focus
>
    <div class="content">
        <div class="left">
            <div
                on:click|stopPropagation={() => dispatch("image", `projects/${content.slug}`)}
                class="image"
                style="
                    background-image: url('/images/projects/{content.slug}.jpg');
                    background-size: cover;
                    background-position: center;
                "
            >
            </div>
        </div>
        <div class="right">
            <h3>{content.name}</h3>
            {#each content.description as paragraph }
                <p>{paragraph}</p>
            {/each}

            {#if content.collaborators.length > 0}
                <h5>Collaborators:</h5>
                {#each content.collaborators as c }
                    <a on:click|preventDefault|stopPropagation={() => dispatch("browser", c.url)} href={c.url}>{c.name}</a>
                {/each}
            {/if}

            {#if content.clients.length > 0}
                <h5>Clients:</h5>
                {#each content.clients as c }
                    <a on:click|preventDefault|stopPropagation={() => dispatch("browser", c.url)} href={c.url}>{c.name}</a>
                {/each}
            {/if}

            {#if content.sponsors.length > 0}
                <h5>Powered by:</h5>
                {#each content.sponsors as c }
                    <a on:click|preventDefault|stopPropagation={() => dispatch("browser", c.url)} href={c.url}>{c.name}</a>
                {/each}
            {/if}
        </div>
    </div>
</Window>