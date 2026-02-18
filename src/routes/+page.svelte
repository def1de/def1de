<script lang="ts">
	import { ScrollProgress } from '$lib/components/magic/scroll-progress';

	import Header from './Header.svelte';
	import Aboutme from './Aboutme.svelte';
	import Skills from './Skills.svelte';
	import Projects from './Projects.svelte';
</script>

<ScrollProgress class="top-0 z-100" />

<Header />

<div class="w-full flex justify-center">
	<div class="w-full flex flex-col gap-3 px-2 md:w-[80%]">
		<Aboutme />
		<Skills />
		<Projects />
	</div>
</div>

<footer class="flex flex-col md:flex-row gap-3 items-center justify-around w-full py-4 text-sm">
	<p>Illia Katerynych 2026</p>
</footer>
