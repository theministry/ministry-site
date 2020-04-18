<script>
    import { onMount, tick } from 'svelte'
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    export let data = "";
    export let type = "";

    let open = false;

    let left;
    let button;

    function openMenu() {
        open = !open
        left = button.offsetLeft;

        document.addEventListener("click", closeMenu)
    }

    function closeMenu() {
        open = false
        document.removeEventListener("click", closeMenu)
    }
</script>

<style>
    div {
        height: 100%;
        display: flex;
        align-items: center;
        padding: 0 4px;
    }

    div:hover {
        background-color: black;
        color: white;
    }

    .active {
        background-color: black;
        color: white;
    }

    nav {
        position: absolute;
        top: 32px;
        display: flex;
        flex-direction: column;
        border: 2px solid black;
        padding: 4px 0;
        background-color: white;
    }

    li {
        background-color: white;
        color: black;
        list-style: none;
        padding: 4px 8px;
    }

    li:hover {
        background-color: black;
        color: white;
    }
</style>

<div
    on:click|stopPropagation={openMenu}
    bind:this={button}
    class="{ open ? "active" : "" }"
>
    <slot></slot>
</div>

{#if open}
    <nav style="left: {left}px;">
        {#each data as item}
            <li on:click={() => dispatch("open", { title:item.name, type:type, content:item })}>{ item.name }</li>
        {/each}
    </nav>
{/if}