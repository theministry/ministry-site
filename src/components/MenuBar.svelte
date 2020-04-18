<script>
    import { slide } from 'svelte/transition';
    export let data;

    import MenuItem from './MenuItem.svelte'
    import Clock from './Clock.svelte'

    console.log(data.studio)
</script>

<style>
    header {
        font-family: "Chicago", monospace;
        height: 32px;
        width: 100%;
        position: absolute;
        top: 0;
        left: 0;
        border-bottom: 2px solid black;
        display: flex;
        flex-direction: row;
        align-items: center;
        background-color: white;

        z-index: 1000000000;
    }
</style>

<header
    in:slide
>
    <!-- system menu -->
    <MenuItem
        type="about"
        on:open
    >
        🚀
    </MenuItem>
    <MenuItem
        data={[data.studio[1]]}
        type="about"
        on:open
    >
        Studio
    </MenuItem>
    <MenuItem
        data={data.projects}
        type="project"
        on:open
    >
        Projects
    </MenuItem>
    <MenuItem
        data={[data.studio[2]]}
        type="mail"
        on:open
    >
        Contact
    </MenuItem>

    <Clock />
</header>