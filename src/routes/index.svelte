<script context="module" lang="ts">
	export const prerender = false;
	export const ssr = false;
</script>
<script lang="ts">
	import { onMount } from "svelte";
  import { browser } from "$app/env";
	import showdown from "showdown";

  let markdownComponent;

  if (browser) {
    onMount(async () => {
      markdownComponent = (await import("$lib/Markdown.svelte")).default;
    });
  }

	let preview = '';
	function convertMarkdown(ev: CustomEvent) {
		const converter = new showdown.Converter();
		preview = converter.makeHtml(ev.detail);
	}
</script>

<svelte:head>
	<title>Petit-Consomacteur</title>
</svelte:head>

<section>
	<h1>
		Bienvenue petit consomacteur !
	</h1>

	<div class="block">
		Explication ici
	</div>
	
	<div class="block">
		Options à paramétrer ici
	</div>

	<div class="block">
		<textarea id="markdown"></textarea>	
		{#if markdownComponent}
			<svelte:component on:easyChange={(event) => { convertMarkdown(event); }} this={markdownComponent} />
		{/if}
	</div>

	<div class="block">
		<div class="editor-preview">
			{@html preview }
		</div>
	</div>

	<div class="block">
		Sauvegarder sa page ici
	</div>
</section>

<style>
	h1 {
		font-size: 1.5rem;
		font-weight: 600;
	}

	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 1;
		margin-top: 100px;
	}

	.block {
		display: flex;
		background-color: white;
		width: 100%;
		height: 100%;
		margin: 12px;
		padding: 24px;
		border-radius: 5px;
	}

	.EasyMDEContainer {
    width: 100%;
  }
</style>
