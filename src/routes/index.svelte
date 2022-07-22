<script context="module" lang="ts">
	export const prerender = true;
</script>

<script lang="ts">
	import Counter from '$lib/Counter.svelte';

	const pathPrefix = './_components';
	const fileNames = ['component1.svelte', 'component2.svelte', 'component3.svelte'];

	let fileIdx = 0;

	let component;

	// 	let Chatbox;

	// function loadChatbox() {
	// 	import('./ChatBox.svelte').then(res => Chatbox = res.default)
	// }

	function nextComponent() {
		if (fileIdx < fileNames.length - 1) {
			fileIdx++;
		} else fileIdx = 0;
		console.log(fileIdx);
		import(`${pathPrefix}/${fileNames[fileIdx]}`).then((res) => (component = res.default));
	}
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<h1>
		<span class="welcome">
			<picture>
				<source srcset="svelte-welcome.webp" type="image/webp" />
				<img src="svelte-welcome.png" alt="Welcome" />
			</picture>
		</span>

		to your new<br />SvelteKit app
	</h1>

	<h2>
		try editing <strong>src/routes/index.svelte</strong>
	</h2>

	<!-- <Component1 /> -->
	{#await import(/* @vite-ignore */ `${pathPrefix}/${fileNames[fileIdx]}`) then value}
		<svelte:component this={component} />
	{/await}

	<button on:click={nextComponent}>Next</button>
	<Counter />
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
