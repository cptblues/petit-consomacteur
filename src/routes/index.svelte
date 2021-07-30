<script context="module" lang="ts">
	export const prerender = false;
	export const ssr = false;
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
		<div class="flex flex-row justify-between w-full">
			<div class="flex flex-col">
				Alignement du texte:
				<select name="alignment" id="alignment">
					<option value="left">Gauche</option>
					<option value="center">Centre</option>
					<option value="right">Droite</option>
				</select>

				Couleur des titres :
			</div>
			<div class="flex flex-col">
				<div>Couleur du texte : </div>
				<div>Couleur de fond : </div>
			</div>
		</div>
		

		
	</div>

	<div class="block">
		<div class="flex flex-row"></div>
		<textarea id="markdown"></textarea>	
		{#if markdownComponent}
			<svelte:component on:easyChange={convertToHtml} this={markdownComponent} />
		{/if}
		<div id="preview" class="custom-preview">{@html preview}</div>
	</div>

	<div class="block">
		Sauvegarder sa page ici
	</div>
</section>

<style lang="scss">

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

</style>

<script lang="ts">
	import { onMount } from "svelte";
  import { browser } from "$app/env";
	import showdown from "showdown";

  let markdownComponent;

  if (browser) {
    onMount(async () => {
      markdownComponent = (await import("$lib/Markdown.svelte")).default;

			const alignment = <HTMLInputElement>document.getElementById('alignment');
			const previewZone = <HTMLInputElement>document.getElementById('preview');

			if (alignment) {
				alignment.addEventListener('change', function() {
					const value = this.value;
					if(value === 'left') {
						previewZone.classList.remove('align_right')
						previewZone.classList.remove('align_center')
						previewZone.classList.add('align_left');
					}
					else if(value === 'right') {
						previewZone.classList.remove('align_left')
						previewZone.classList.remove('align_center')
						previewZone.classList.add('align_right');
					}
					else if(value === 'center') {
						previewZone.classList.remove('align_right')
						previewZone.classList.remove('align_left')
						previewZone.classList.add('align_center');
					}
				});
			}
    });
  }

	let preview = '';
	function convertToHtml(ev: CustomEvent) {
		const converter = new showdown.Converter();
		converter.setOption('completeHTMLDocument', true);
		converter.setOption('simpleLineBreaks', true);
		preview = converter.makeHtml(ev.detail);
	}
	
</script>