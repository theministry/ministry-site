<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    export let title;
    export let type;
    export let content;
</script>

<style>
    div {
        width: 64px;
        margin: 8px;
        height: 80px;
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    svg {
        width: 64px;
        height: 64px;
    }

    span {
        background-color: white;
        color: black;
        overflow-x: visible;
        text-align: center;
        height: 16px;
        font-size: 16px;
        line-height: 1;
        min-width: 100%;
        width: auto;
        font-size: bold;
    }
</style>

<div
    on:click|stopPropagation={() => {console.log("hi"); dispatch("open", {title:title, type:type, content:content})}}
>
    <svg width="100%" height="100%" viewBox="0 0 128 128" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:space="preserve" xmlns:serif="http://www.serif.com/" style="fill-rule:evenodd;clip-rule:evenodd;stroke-miterlimit:1.5;">
        <rect id="file" x="0" y="0" width="128" height="128" style="fill:none;"/>
        <path d="M86.966,16.135L106.077,35.246L106.077,115.162L27.728,115.162L27.728,16.135L86.966,16.135Z" style="fill:#fff;stroke:#000;stroke-width:4px;"/>
        <path d="M106.077,35.246L86.966,16.135L86.966,35.246L106.077,35.246" style="fill:none;stroke:#000;stroke-width:4px;"/>
        <path d="M61.51,33.949L61.51,55.442" style="fill:none;stroke:#000;stroke-width:4px;"/>
        <path d="M72.295,33.949L72.295,55.22" style="fill:none;stroke:#000;stroke-width:4px;"/>
        <path d="M51.432,48.529L51.432,64L82.373,64L82.373,48.529" style="fill:none;stroke:#000;stroke-width:4px;"/>
        <path d="M39.829,100.73L93.976,100.73" style="fill:none;stroke:#000;stroke-width:4px;"/>
        <path d="M39.829,89.441L93.976,89.441" style="fill:none;stroke:#000;stroke-width:4px;"/>
        <path d="M39.829,78.152L93.976,78.152" style="fill:none;stroke:#000;stroke-width:4px;"/>
    </svg>

    <span contenteditable>{title}</span>
</div>