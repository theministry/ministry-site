<script>
	import data from './data/data.json'

	import MenuBar from './components/MenuBar.svelte'
	import Intro from './components/Intro.svelte'

	import Window from './components/Window.svelte'
	import Project from './components/Project.svelte'
	import Alert from './components/Alert.svelte'
	import Email from './components/Email.svelte'
	import Folder from './components/Folder.svelte'
	import ImageViewer from './components/ImageViewer.svelte'
	import Browser from './components/Browser.svelte'
	import About from './components/About.svelte'
	import Mail from './components/Mail.svelte'

	import DesktopIcon from './components/DesktopIcon.svelte'

	let intro = true;

	let id = 1;
	let windows = [];

	const openWindow = (e, title, type, content) => {
		console.log('opening')
		console.log(e)
		console.log(title)
		console.log(type)
		console.log(content)

		windows = [...windows, {
			title: title,
			type: type,
			content: content,
			id: id
		}]
		id += 1;
	}

	const closeWindow = (e, id) => {
		windows = windows.filter(w => w.id !== id);
	}

	const focusWindow = (e, id) => {
		let win = windows.filter(w => w.id === id)[0]
		windows = [...windows.filter(w => w.id !== id), win];
	}
</script>

<style>
	div.desktop {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-image: url("/images/wallpaper.jpg");
		background-position: center;
		background-size: cover;
	}
</style>

<!-- desktop -->
<div class="desktop"></div>

<!-- intro -->
{#if intro}
	<Intro
		on:close={(e) => intro = false}
	/>
{/if}

{#if !intro}

<!-- desktop icons -->
<DesktopIcon
	icon="happycomputer"
	name="studio"
	on:open={(e) => openWindow(e, "🗂 /ministry/"+e.detail, "folder", e.detail)}
	pos={{
		top: 64,
		left: window.innerWidth - 64 - 16,
	}}
/>

<DesktopIcon
	icon="projects"
	name="projects"
	on:open={(e) => openWindow(e, "🗂 /ministry/"+e.detail, "folder", e.detail)}
	pos={{
		top: 64 + 64 + 32,
		left: window.innerWidth - 64 - 16,
	}}
/>

<DesktopIcon
	icon="trash"
	name="trash"
	on:open={(e) => openWindow(e, "🗂 /ministry/"+e.detail, "folder", e.detail)}
	pos={{
		top: window.innerHeight - 64 - 32,
		left: window.innerWidth - 64 - 16,
	}}
/>

<!-- manubar -->
<MenuBar
	data={data}
	on:open={(e) => openWindow(e, e.detail.title, e.detail.type, e.detail.content)}
/>

{console.log(windows)}
{#each windows as window, i (window.id)}

	{#if window.type === "project"}
	<Project
		id={window.id}
		title={window.title}
		content={window.content}
		on:focus={(e) => focusWindow(e, window.id)}
		on:close={(e) => closeWindow(e, window.id)}
		on:image={(e) => openWindow(e, "ImageViewer: " + e.detail + ".jpg", "image", e.detail)}
		on:browser={(e) => openWindow(e, "", "browser", e.detail)}
	/>
	{:else if window.type === "email"}
	<Email
		id={window.id}
		title={window.title}
		content={window.content}
		on:focus={(e) => focusWindow(e, window.id)}
		on:close={(e) => closeWindow(e, window.id)}
	/>
	{:else if window.type === "image"}
	<ImageViewer
		id={window.id}
		title={window.title}
		content={window.content}
		on:focus={(e) => focusWindow(e, window.id)}
		on:close={(e) => closeWindow(e, window.id)}
	/>
	{:else if window.type === "browser"}
	<Browser
		id={window.id}
		title={window.title}
		content={window.content}
		on:focus={(e) => focusWindow(e, window.id)}
		on:close={(e) => closeWindow(e, window.id)}
	/>
	{:else if window.type === "about"}
	<About
		id={window.id}
		title={window.title}
		content={window.content}
		on:focus={(e) => focusWindow(e, window.id)}
		on:close={(e) => closeWindow(e, window.id)}
		on:image={(e) => openWindow(e, "ImageViewer: " + e.detail + ".jpg", "image", e.detail)}
	/>
	{:else if window.type === "folder"}
	<Folder
		id={window.id}
		title={window.title}
		content={window.content}
		on:focus={(e) => focusWindow(e, window.id)}
		on:close={(e) => closeWindow(e, window.id)}
		on:open={(e) => openWindow(e, e.detail.title, e.detail.type, e.detail.content)}
	/>
	{:else if window.type === "mail"}
	<Mail
		id={window.id}
		title={window.title}
		content={window.content}
		on:focus={(e) => focusWindow(e, window.id)}
		on:close={(e) => closeWindow(e, window.id)}
	/>
	{:else}
	<Window
		id={window.id}
		title={window.title}
		on:focus={(e) => focusWindow(e, window.id)}
		on:close={(e) => closeWindow(e, window.id)}
		controls={true}
	>
		<p>{window.content}</p>
	</Window>
	{/if}
{/each}
{/if}