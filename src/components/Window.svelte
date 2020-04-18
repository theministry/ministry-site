<script>
    import { createEventDispatcher } from 'svelte';
    import { scale } from 'svelte/transition';
    const dispatch = createEventDispatcher();

    let posDeviation = Math.floor(Math.random() * 16) * 10 - 80

    export let id
    export let title
    export let controls = false
    export let size = {
        height: window.innerHeight - 32 - 8 < 240 ? 320 : 240,
        width: window.innerWidth - 8 < 640 ? window.innerWidth - 8 : 640,
        minWidth: 200,
        minHeight: 150,
        maximised: false
    }
    export let pos = {
        top: window.innerHeight / 2 - size.height / 2 + 16 + posDeviation,
        left: window.innerWidth / 2 - size.width / 2 + posDeviation,
        }

    let dragging = false;
    let resizing = false;
    let o = { x:0, y:0 }

    function startDrag(e) {
        dragging = true;
        o.y = e.pageY - pos.top
        o.x = e.pageX - pos.left
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

    function startResize(e) {
        resizing = true;
        o.y = size.height + pos.top - e.pageY
        o.x = size.width + pos.left - e.pageX
        document.addEventListener("mousemove", resize)
        document.addEventListener("touchmove", resize)
        document.addEventListener("mouseup", endResize)
        document.addEventListener("touchend", endResize)
    }

    function resize(e) {
        size.height = e.pageY - pos.top + o.y;
        size.width = e.pageX - pos.left + o.x;

        if (size.height < size.minHeight) size.height = size.minHeight
        if (size.width < size.minWidth) size.width = size.minWidth
        e.preventDefault()
    }

    function endResize(e) {
        resizing = false;
        document.removeEventListener("mousemove", resize)
        document.removeEventListener("touchmove", resize)
        document.removeEventListener("mouseup", endResize)
        document.removeEventListener("touchend", endResize)
    }

    function maximise(e) {
        size.maximised = !size.maximised
    }
</script>

<style>
    article {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        border: 2px solid black;
        padding: 4px;

        background-color: white;

        position: absolute;
        border-radius: 10px 10px 10px 10px;
    }

    article.dragging {
        border: 2px dotted black;
    }

    article.dragging button, article.resizing button {
        display: none;
    }

    article.resizing {
        border: 2px dotted black;
    }

    header {
        position: absolute;
        height: 20px;
        width: 100%;
        left: 0;
        top: 0;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between;
        cursor: move;
    }

    h3 {
        text-align: center;
        margin: auto;
    }

    footer {
        position: absolute;
        height: 20px;
        width: 100%;
        left: 0;
        bottom: 0;
        display: flex;
        flex-direction: row;
        align-items: center;
        justify-content: space-between
    }

    p {
        text-align: center;
        margin: auto;
    }

    button {
        width: 16px;
        height: 16px;
        padding: 0;
        border-radius: 1000px;
        border: 2px solid black;
        margin: 2px;
    }

    button.resize {
        background-color: #6DDA41;
        cursor: nwse-resize;
        margin-left: auto;
    }

    button.close {
        background-color: #FF3B38
    }

    button.maximise {
        background-color: #FFDA41
    }

    button.info {
        background-color: #44B8FF
    }
</style>

<article
    style='
        top:{
            size.maximised ?
            32 + 4 :
            pos.top
        }px;
        left:{
            size.maximised ?
            0 + 4 :
            pos.left
        }px;
        height:{
            size.maximised ?
            window.innerHeight - 32 - 8 :
            size.height
        }px;
        width:{
            size.maximised ?
            window.innerWidth - 8 :
            size.width
        }px;
    '
    on:click={() => dispatch('focus')}
    class='
        {dragging && "dragging"}
        {resizing && "resizing"}
    '
    transition:scale={{
        duration: 200
    }}
>
    <header
        on:mousedown|preventDefault={startDrag}
        on:touchstart|preventDefault={startDrag}
    >
        {#if controls}
        <button
            class="close"
            on:click|stopPropagation={() => dispatch('close')}
            on:mousedown|stopPropagation
            on:touchstart|stopPropagation
        />
        {/if}
        <h3>{title}</h3>
        {#if controls}
        <button
            class="maximise"
            on:click|stopPropagation={maximise}
            on:mousedown|stopPropagation
            on:touchstart|stopPropagation
        />
        {/if}
    </header>

    <slot>
        <p>Empty window.</p>
    </slot>

    <footer>
        {#if controls}
        <!-- <button class="info" /> -->
        <button
            class="resize"
            on:mousedown|stopPropagation={startResize}
            on:touchstart|stopPropagation={startResize}
        />
        {/if}
    </footer>
</article>