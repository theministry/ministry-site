<script>
    import Window from './Window.svelte'
    import { fly } from 'svelte/transition';
    import { createEventDispatcher } from 'svelte';

    import Bits from './icons/Bits.svelte'
    import Atoms from './icons/Atoms.svelte'

    const dispatch = createEventDispatcher();

    const size = {
        height: window.innerHeight - 32 - 8 < 240 ? window.innerHeight - 32 - 8 : window.innerWidth < 420 ? 420 : 240,
        width: window.innerWidth - 8 < 640 ? window.innerWidth - 8 : 640,
    }

    const pos = {
        top: window.innerHeight / 2 - size.height / 2 + 16,
        left: window.innerWidth / 2 - size.width / 2,
    }

</script>

<style>
    main {
        position: relative;
        width: 100%;
        height: 100%;
        font-size: 20px;
        line-height: 2;
        margin: 0 4px;
        border: 4px solid black;
        border-radius: 6px;
        padding: 32px;
        display: flex;
        align-items: center;
    }

    div.text {
        flex-direction: column;
        align-items: center;
    }

    button {
        position: absolute;
        bottom: 16px;
        right: 16px;
        border: none;
        background-color: #078DFF;
        color: white;
        border-radius: 1000px;
        font-family: "Chicago", monospace;
        font-size: 16px;
        letter-spacing: 1px;
        padding: 4px 32px;
    }

    button:hover {
        background-color: #003DFF;
    }

    span {
        display: inline-block;
        font-weight: bold;
        letter-spacing: 2px;
    }
</style>

<Window
	id={0}
	title={""}
	on:focus={(e) => {}}
	on:close={(e) => {}}
	controls={false}
    size={size}
    pos={pos}
>
	<main>
		<div class="text">
            <p><span>The Ministry of Extraordinary Affairs</span> is a design studio that mashes <Bits /> and <Atoms /> together into interactive products and art installations.</p>
		</div>
        <button
            on:click={(e) => dispatch("close")}
        >
            let's go
        </button>
	</main>
</Window>