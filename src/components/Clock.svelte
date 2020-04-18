<script>
    import { onMount } from 'svelte'
    let clock = "00:00 AM"

    onMount(() => {
        const interval = setInterval(() => {
            clock = new Date(Date.now()).toLocaleTimeString();
        }, 1000)
    }
    )
</script>

<style>
    div {
        margin-left: auto;
        margin-right: 8px;
    }
</style>

<div>
    { clock }
</div>