# sv5tiptap - A simple rich editor for svelte 5

This component library is not a perfect editor, and compared to other open-source projects, its features are quite limited. The main goal of this small project is to provide a basic rich editor for your Svelte development or testing with Tiptap.

**sv5tiptap** is primarily based on Svelte 5, Tiptap 2, Tailwind 4, DaisyUI 5, Lucide icons and was developed using the latest versions of these frameworks, as detailed in the `package.json`. It does not rely on many custom extensions; only two existing open-source extensions were used to implement image and font size functionality. If you need more features, you are welcome to develop extensions yourself. Tiptap provides detailed documentation for this, though it can be a time-consuming challenge.

Currently, there is no user manual, and the code lacks comments, as I haven’t had enough time to complete this yet. However, I plan to continue optimizing it and add clear documentation after using it for a short period in my project. Although there are no official documents yet, most of the code follows the basic usage of Svelte, Tiptap, and Tailwind.

At this moment, **sv5tiptap** may not be perfect, but for me and many users, it indeed fills the need for a simple CMS editor within Svelte projects. I hope it proves useful to you or at least inspires you.

## This library is licensed under the MIT License.

Welcome any suggestions or contributions.

## This library uses the following packages. Thanks a lot!

- **Tiptap V2**
- **Tailwind CSS V4**
- **DaisyUI V5**
- **Lucide icons**
- **tiptap-extension-resize-image**: [GitHub](https://github.com/bae-sh/tiptap-extension-resize-image)
- **tiptap-extension-font-size**: [GitHub](https://github.com/TheNaschkatze/tiptap-extension-font-size)

## Installation

```bash
npm install @lux-ok/sv5tiptap
```

also your target project need to installed the following packages:

```json
"peerDependencies": {
  "svelte": "^5.0.0", // dev
  "tailwindcss": "^4.0.0", // dev
  "@tailwindcss/typography": "^0.5.15", // dev
  "daisyui": "^5.0.9", // dev
}
```

## svelte 5 Usage

```svelte
<script lang="ts">
	import { htmlContent, jsonContent, jsonToHtml, TiptapEditor } from '@lux-ok/sv5tiptap';
	import type { EditorType } from '@lux-ok/sv5tiptap';
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
			// callback on editor update
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

	<!-- For demo, not necessary -->
	<div class="prose max-w-full flex-1 overflow-auto rounded-md border p-4">
		{@html html}
	</div>
</div>
```

```css
// src/app.css

@import 'tailwindcss';
@plugin '@tailwindcss/typography';
@plugin "daisyui";
@source "../node_modules/@lux-ok/sv5tiptap";

.prose {
	@apply text-base text-gray-700 dark:text-gray-300;

	h1,
	h2,
	h3 {
		@apply my-3;
	}
	h1 {
		@apply text-primary text-3xl font-bold;
	}
	h2 {
		@apply text-secondary text-2xl font-semibold;
	}
	p {
		@apply leading-relaxed;
	}
	ul {
		@apply marker:text-primary ml-5 list-outside list-disc;
	}
	ol {
		@apply marker:text-secondary ml-5 list-outside list-decimal;
	}
	blockquote {
		@apply border-primary border-l-4 pl-4 text-gray-600 italic dark:text-gray-400;
	}
	li p {
		@apply my-2;
	}
	hr {
		@apply my-3;
	}
	table {
		@apply table w-full rounded-lg border border-gray-300 dark:border-gray-600;
	}
	col {
		@apply w-auto;
	}
	th {
		@apply bg-base-200 dark:bg-base-300 border border-gray-300 p-2 text-base font-semibold dark:border-gray-600;
	}
	td {
		@apply border border-gray-300 p-2 dark:border-gray-600;
	}
	th p,
	td p {
		@apply my-0 min-h-6;
	}
	pre code {
		@apply overflow-hidden text-wrap;
	}
	img {
		@apply mx-0 my-4;
	}
}
```
