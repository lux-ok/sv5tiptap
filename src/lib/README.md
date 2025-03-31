# sv5tiptap - A simple rich editor for svelte 5

This component library is not a perfect editor, and compared to other open-source projects, its features are quite limited. The main goal of this small project is to provide a simple starting point for a basic editor or to serve as a simple starting point for your Svelte development or testing with Tiptap.

**sv5tiptap** is primarily based on Svelte 5, Tiptap 2, Tailwind 4, and DaisyUI 5, and was developed using the latest versions of these frameworks, as detailed in the `package.json`. It does not rely on many custom extensions; only two existing open-source extensions were used to implement image and font size functionality. If you need more features, you are welcome to develop extensions yourself. Tiptap provides detailed documentation for this, though it can be a time-consuming challenge.

Currently, there is no user manual, and the code lacks comments, as I haven’t had enough time to complete this yet. However, I plan to continue optimizing it and add clear documentation after using it for a short period in my project. Although there are no official documents yet, most of the code follows the basic usage of Svelte, Tiptap, and Tailwind.

At this moment, **sv5tiptap** may not be perfect, but for me and many users, it indeed fills the need for a simple CMS editor within Svelte projects. I hope it proves useful to you or at least inspires you.

## This library is licensed under the MIT License.

Welcome any suggestions or contributions.

## This library uses the following packages. Thanks a lot!

- **Tiptap V2**
- **Tailwind CSS V4**
- **DaisyUI V5**
- **tiptap-extension-resize-image**: [GitHub](https://github.com/bae-sh/tiptap-extension-resize-image)
- **tiptap-extension-font-size**: [GitHub](https://github.com/TheNaschkatze/tiptap-extension-font-size)

## Installation

```bash
npm install @lux-ok/sv5tiptap
```

also you need to install the following packages:

"peerDependencies": {
"svelte": "^5.0.0",
"tailwindcss": "^4.0.0",
"@tailwindcss/typography": "^0.5.15",
"daisyui": "^5.0.9"
}

## Usage

```svelte
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
```
