<script>
    import Window from './Window.svelte'
    export let title;
    export let content;
    export let id;
</script>

<style>
    div {
        margin-top: 22px;
        /* margin-bottom: 16px; */
        border-radius: 4px;
        border: 2px solid black;
        width: 100%;
        height: 100%;
    }
</style>

<Window
    id={id}
    title={title}
    controls={true}

    on:close
    on:focus
>
    <div
        style="
            background-image: url('/images/{content}.jpg');
            background-size: cover;
            background-position: center;
        "
    />
</Window>