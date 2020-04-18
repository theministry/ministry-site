<script>
    import { createEventDispatcher } from 'svelte';
    import { scale } from 'svelte/transition';
    const dispatch = createEventDispatcher();

    export let size = {
        width: 64,
        height: 80,
    }
    export let pos = {
        top: 10,
        left: 10,
    }

    export let icon = "happycomputer"
    export let name = "Studio"

    let dragging = false;

    let o = { x:0, y:0 }

    function startDrag(e) {
        dragging = true;
        o.y = e.pageY - pos.top
        o.x = e.pageX - pos.left

        document.addEventListener("mouseup", doOpen)
        document.addEventListener("touchend", doOpen)

        document.addEventListener("mousemove", doDrag)
        document.addEventListener("touchmove", doDrag)
    }

    function doOpen(e) {
        document.removeEventListener("mousemove", doDrag)
        document.removeEventListener("touchmove", doDrag)
        document.removeEventListener("mouseup", doOpen)
        document.removeEventListener("touchend", doOpen)

        console.log("opening")
        dispatch("open", name)
    }

    function doDrag(e) {
        console.log("dragging")
        document.removeEventListener("mousemove", doDrag)
        document.removeEventListener("touchmove", doDrag)
        document.removeEventListener("mouseup", doOpen)
        document.removeEventListener("touchend", doOpen)

        document.addEventListener("mousemove", drag)
        document.addEventListener("touchmove", drag)
        document.addEventListener("mouseup", endDrag)
        document.addEventListener("touchend", endDrag)
    }

    function drag(e) {
        pos.top = e.pageY - o.y;
        pos.left = e.pageX - o.x;
        e.preventDefault()
    }

    function endDrag(e) {
        dragging = false;
        document.removeEventListener("mousemove", drag)
        document.removeEventListener("touchmove", drag)
        document.removeEventListener("mouseup", endDrag)
        document.removeEventListener("touchend", endDrag)
    }

</script>

<style>
    div {
        position: absolute;
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
    style='
        top:{pos.top}px;
        left:{pos.left}px;
        height:{size.height}px;
        width:{size.width}px;
    '
    on:mousedown={startDrag}
    on:touchstart={startDrag}
    class=''
    transition:scale={{
        duration: 200
    }}
>
    {#if icon === "happycomputer"}

    <svg width="100%" height="100%" viewBox="0 0 128 128" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:space="preserve" xmlns:serif="http://www.serif.com/" style="fill-rule:evenodd;clip-rule:evenodd;stroke-miterlimit:1.5;">
        <rect id="computer" x="0" y="0" width="128" height="128" style="fill:none;"/>
        <clipPath id="_clip1">
            <rect x="0" y="0" width="128" height="128"/>
        </clipPath>
        <g clip-path="url(#_clip1)">
            <path d="M24.333,100.885L17.588,125.882L33.059,110.412L48.529,100.885" style="fill:#fff;stroke:#000;stroke-width:4px;"/>
            <path d="M103.667,100.885L110.412,125.882L94.941,110.412L79.471,100.885" style="fill:#fff;stroke:#000;stroke-width:4px;"/>
            <path d="M99.574,11.645L28.426,11.645L24.333,100.885L103.667,100.885L99.574,11.645Z" style="fill:#fff;stroke:#000;stroke-width:4px;"/>
            <rect x="36.927" y="23.504" width="54.147" height="47.935" style="fill:#fff;stroke:#000;stroke-width:4px;"/>
            <path d="M52.881,100.885L45.145,108.336L83.822,108.336L76.086,100.885L52.881,100.885Z" style="fill:#fff;stroke:#000;stroke-width:4px;"/>
            <path d="M64,2.118L71.735,11.645L71.735,17.588L56.265,17.588L56.265,11.645L64,2.118Z" style="fill:#fff;stroke:#000;stroke-width:4px;"/>
            <path d="M56.265,87.206L91.073,87.206" style="fill:none;stroke:#000;stroke-width:4px;"/>
            <path d="M36.927,87.206L40.794,87.206" style="fill:none;stroke:#000;stroke-width:4px;"/>
            <circle cx="64" cy="11.645" r="2.374"/>
            <path d="M58.608,31.125L58.608,52.619" style="fill:none;stroke:#000;stroke-width:4px;"/>
            <path d="M69.392,31.125L69.392,52.397" style="fill:none;stroke:#000;stroke-width:4px;"/>
            <path d="M48.529,45.706L48.529,61.177L79.471,61.177L79.471,45.706" style="fill:none;stroke:#000;stroke-width:4px;"/>
        </g>
    </svg>

    {:else if icon === "projects"}

    <svg width="100%" height="100%" viewBox="0 0 128 128" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:space="preserve" xmlns:serif="http://www.serif.com/" style="fill-rule:evenodd;clip-rule:evenodd;stroke-miterlimit:1.5;">
        <rect id="projects" x="0" y="0" width="128" height="128" style="fill:none;"/>
        <rect x="20.802" y="24.26" width="84.852" height="76.624" style="fill:#fff;"/>
        <path d="M14.702,117.155L16.43,84.474L18.797,62.005L18.208,47.466L16.214,36.155L17.649,21.595L20.672,13.754L25.587,9.087L33.403,6.502L91.343,5.381L99.614,7.025L104.469,12.775L107.128,20.123L108.137,37.646L108.357,45.35L109.056,58.493L107.565,74.067L109.061,86.028L110.494,98.466L113.298,112.81L111.675,122.619L105.867,122.457L104.348,101.513L101.454,100.552L67.839,108.66L39.265,106.271L25.3,106.133L24.341,122.095L17.353,121.283L14.702,117.155ZM24.84,33.382L23.425,86.336L24.459,89.625L29.504,87.574L31.839,92.356L37.254,88.909L40.631,96.143L45.784,90.542L47.234,91.593L49.522,95.834L54.863,91.225L58.771,95.829L64,93.472L66.809,97.374L70.952,93.034L75.027,95.255L80.942,92.426L82.354,94.087L86.018,90.814L90.807,91.928L96.502,88.845L101.797,90.749L101.41,75.529L97.646,49.799L99.197,39.41L99.045,36.99L93.761,39.339L91.575,43.52L87.138,40.285L84.208,39.344L79.721,42.896L76.828,39.584L71.876,43.648L66.809,39.53L64,42.46L58.239,38.361L54.754,41.68L50.386,36.158L47.092,38.689L43.313,35.379L39.688,39.722L37.422,34.154L32.886,39.031L31.365,35.637L26.896,40.248L25.854,40.248L24.84,33.382Z" style="fill:#fff;stroke:#000;stroke-width:4px;"/>
        <path d="M37.441,17.688C38.746,16.79 42.508,18.427 43.345,20.118C44.181,21.809 42.878,25.699 42.878,25.699C41.342,26.659 39.621,27.196 37.242,26.227C35.407,25.243 35.163,23.473 34.987,21.668C34.987,21.668 36.136,18.586 37.441,17.688Z"/>
        <path d="M88.553,26.424C87.033,25.978 85.931,22.026 86.716,20.31C87.5,18.595 91.341,17.153 91.341,17.153C93.657,17.983 95.077,19.278 95.305,21.194C95.085,23.131 94.34,24.64 93.19,25.819C93.19,25.819 90.073,26.871 88.553,26.424Z"/>
    </svg>

    {:else if icon === "trash"}

    <svg width="100%" height="100%" viewBox="0 0 128 128" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" xml:space="preserve" xmlns:serif="http://www.serif.com/" style="fill-rule:evenodd;clip-rule:evenodd;stroke-miterlimit:1.5;">
        <rect id="trash" x="0" y="0" width="128" height="128" style="fill:none;"/>
        <path d="M99.574,116.704L28.426,116.704L24.333,27.464L103.667,27.464L99.574,116.704Z" style="fill:#fff;stroke:#000;stroke-width:4px;"/>
        <path d="M102.915,19.38L25.085,19.38L20.608,27.464L107.392,27.464L102.915,19.38Z" style="fill:#fff;stroke:#000;stroke-width:4px;"/>
        <path d="M84.334,11.296L43.666,11.296L41.326,19.38L86.674,19.38L84.334,11.296Z" style="fill:#fff;stroke:#000;stroke-width:4px;"/>
        <path d="M36.485,34.897L39.485,107.944" style="fill:none;stroke:#000;stroke-width:4px;"/>
        <path d="M50.742,34.897L51.742,107.944" style="fill:none;stroke:#000;stroke-width:4px;"/>
        <path d="M64,34.897L64,107.944" style="fill:none;stroke:#000;stroke-width:4px;"/>
        <path d="M77.258,34.897L76.258,107.944" style="fill:none;stroke:#000;stroke-width:4px;"/>
        <path d="M91.515,34.897L88.515,107.944" style="fill:none;stroke:#000;stroke-width:4px;"/>
    </svg>

    {/if}

    <span contenteditable>{name}</span>
</div>

