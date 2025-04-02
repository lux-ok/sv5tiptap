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
	let html = $state<string>();

	onMount(() => {
		// This is not necessary, you can use getJSON() or getHTML() anytime like save json to database
		html = jsonToHtml(jsonContent);
		editor?.on('update', () => {
			console.log('updated');
			html = jsonToHtml(editor?.getJSON());
		});
	});
</script>

<div class="flex h-svh flex-row gap-4 overflow-hidden p-4">
	<TiptapEditor
		bind:editor
		{content}
		defaultToolbar={true}
		class="flex-1 rounded-md"
		editorClass="rounded-b-xs"
	/>

	<!-- This is WYSWYG demo, not necessary -->
	<div class="prose max-w-full flex-1 overflow-auto rounded-md border p-4">
		{@html html}
	</div>
</div>
