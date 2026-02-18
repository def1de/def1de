<script lang="ts">
	import { onMount } from 'svelte';
	import { marked, type Tokens } from 'marked';
	import DOMPurify from 'dompurify';
	import Glass from '$lib/Glass.svelte';

	const README_URL = 'https://raw.githubusercontent.com/def1de/def1de/refs/heads/main/README.md';

	// Helps relative links/images in README render correctly on your site
	const BASE_BLOB = 'https://github.com/def1de/def1de/blob/main/';
	const BASE_RAW = 'https://raw.githubusercontent.com/def1de/def1de/main/';

	let html = '';
	let loading = true;
	let error: string | null = null;

	const isAbsolute = (url: string) =>
		/^[a-z][a-z0-9+.-]*:\/\//i.test(url) || url.startsWith('mailto:');

	onMount(async () => {
		try {
			const res = await fetch(README_URL, { cache: 'no-cache' });
			if (!res.ok) throw new Error(`Failed to load README (${res.status})`);

			const md = await res.text();

			const renderer = new marked.Renderer();

			renderer.link = function ({ href, title, tokens }: Tokens.Link): string {
				let url = href ?? '';
				if (url && !isAbsolute(url) && !url.startsWith('#')) {
					url = BASE_BLOB + url.replace(/^\.?\//, '');
				}

				// Render link text from tokens (handles **bold**, `code`, etc.)
				const text = this.parser?.parseInline(tokens) ?? '';

				const t = title ? ` title="${title.replace(/"/g, '&quot;')}"` : '';
				return `<a href="${url}"${t} target="_blank" rel="noopener noreferrer">${text}</a>`;
			};

			renderer.image = ({ href, title, text }: Tokens.Image): string => {
				let url = href ?? '';
				if (url && !isAbsolute(url) && !url.startsWith('data:')) {
					url = BASE_RAW + url.replace(/^\.?\//, '');
				}
				const t = title ? ` title="${title.replace(/"/g, '&quot;')}"` : '';
				const alt = (text ?? '').replace(/"/g, '&quot;');
				return `<img src="${url}" alt="${alt}"${t} loading="lazy" />`;
			};

			const raw = marked.parse(md, { renderer }) as string;

			html = DOMPurify.sanitize(raw, {
				ADD_ATTR: ['target', 'rel']
			});
		} catch (e: any) {
			error = e?.message ?? 'Failed to load README.';
		} finally {
			loading = false;
		}
	});
</script>

<section class="w-full mb-3">
	<div class="mb-6">
		<h2 class="text-2xl font-bold text-surface-50 mb-2">About me</h2>
		<p class="text-sm text-surface-400">
			Welcome to my portfolio. Here you can learn more about my skills, experience, and projects.
		</p>
	</div>

	<Glass className="w-full readme p-6">
		{#if loading}
			<p>Loading…</p>
		{:else if error}
			<p class="error">{error}</p>
		{:else}
			{@html html}
		{/if}
	</Glass>
</section>

<style>
	:global(.readme img) {
		max-width: 100%;
		height: auto;
	}
	:global(.readme pre) {
		overflow: auto;
	}

	:global(.readme ul) {
		list-style: disc;
		padding-left: 1.25rem;
		margin: 0.75rem 0;
	}
	:global(.readme ol) {
		list-style: decimal;
		padding-left: 1.25rem;
		margin: 0.75rem 0;
	}
	:global(.readme li) {
		margin: 0.25rem 0;
	}
	:global(.readme ul ul) {
		list-style: disc;
		margin-top: 0.25rem;
	}

	.error {
		color: #c00;
	}
</style>
