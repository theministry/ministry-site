<script>
    import Window from './Window.svelte'
    export let title;
    export let content;
    export let id;
</script>

<style>
    .browser {
        /* margin-top: 22px; */
        border-radius: 4px;
        border: 2px solid black;
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
    }

    header {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }

    iframe {
        flex-grow: 1;
        border: none;
    }

    header {
        height: 20px;
        width: 100%;
    }

    .buttongroup {
        margin: 2px;
        margin-left: 32px;
        margin-right: 32px;
        padding: 2px;
    }

    .address {
        margin: 0 auto;
        font-size: 12px;
    }
</style>

<Window
    id={id}
    title={title}
    controls={true}

    on:close
    on:focus
>
    <header>
        <div class="address">{content}</div>
    </header>
    <div class="browser">
        <iframe title={title} src={content} />
    </div>
</Window>