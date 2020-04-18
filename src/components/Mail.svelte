<script>
    import Window from './Window.svelte'

    export let id
    export let title
    export let content
</script>

<style>
    p {
        text-align: center;
    }

    a {
        color: #078DFF;
        font-weight: bold;
        text-decoration: none;
    }

    a:hover {
        color: #003DFF;
    }
</style>

<Window
    id={id}
    title={title}
    controls=true

    on:close
    on:focus
>
    <p>We're always interested in new projects.</p>
    <p><a href="mailto:nikolai@theministry.co">Click here to send us an email</a> and start your next adventure!</p>
</Window>