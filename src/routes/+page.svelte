<script lang="ts">
	import { htmlContent, jsonContent, jsonToHtml, TiptapEditor } from '$lib/index.js';
	import type { EditorType } from '$lib/index.js';
	import { onMount } from 'svelte';

	/**
	 * You can put html or json content to display the default content when the editor is instantiated.
	 * If content is set to undefined, sv5tiptap will load the demo content.
	 * or you only need blank content: content = ‘’
	 */
	let content = undefined;
	let editor = $state<EditorType>();
	let html = $state();

	$effect(() => {
		// This is not necessary
		// you can use getJSON() or getHTML() to obtain the data of the editor element when needed.
		editor?.on('update', () => {
			html = jsonToHtml(editor?.getJSON());
		});
	});

	onMount(() => {
		// This is not necessary
		html = jsonToHtml(jsonContent);
	});
</script>

<div class="flex h-svh flex-row gap-4 overflow-hidden p-4">
	<TiptapEditor bind:editor {content} defaultToolbar={true} class="flex-1 rounded-md" />

	<div class="prose max-w-full flex-1 overflow-auto rounded-md border p-4">
		<!-- This is not necessary -->
		{@html html}
	</div>
</div>
