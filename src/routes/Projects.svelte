<script lang="ts">
	import {
		Github,
		PanelTop,
		SquareSigma,
		LayoutTemplate,
		Rocket,
		MessageCircle
	} from '@lucide/svelte';

	import Button from '$lib/Button.svelte';
	import Glass from '$lib/Glass.svelte';

	type ProjectData = {
		title: string;
		icon: typeof SquareSigma;
		description: string;
		tags: string[];
		github: string;
		demo: string;
	};

	let projects: ProjectData[] = [
		{
			title: 'Chat',
			icon: MessageCircle,
			description: 'A messaging application',
			tags: ['rust', 'axum', 'database', 'async'],
			github: 'https://github.com/def1de/chat_app',
			demo: 'https://chat.def1de.com/'
		},
		{
			title: 'Mathsblitz',
			icon: SquareSigma,
			description: 'Daily maths solving game',
			tags: ['python', 'flask', 'svelte'],
			github: 'https://github.com/def1de/mathsblitz',
			demo: ''
		},
		{
			title: 'wwidgt',
			icon: LayoutTemplate,
			description: 'Widget utility for wayland compositors',
			tags: ['c', 'gtk4', 'foss'],
			github: 'https://github.com/def1de/wwidgt',
			demo: ''
		},
		{
			title: 'Space Adrift',
			icon: Rocket,
			description: 'A rogulike game',
			tags: ['c++', 'sfml', 'custom engine'],
			github: 'https://github.com/def1de/space-adrift',
			demo: ''
		}
	];
</script>

<section class="w-full flex-1 mb-3">
	<!-- Section Header -->
	<div class="mb-6">
		<h2 class="text-2xl font-bold text-surface-50 mb-2">Projects</h2>
		<p class="text-sm text-surface-400">The list of my recent projects</p>
	</div>

	<div class="grid grid-cols-1 gap-3 md:grid-cols-2 2xl:grid-cols-4">
		{#each projects as projectd}
			{@render project(projectd)}
		{/each}
	</div>
</section>

{#snippet project(projectdata: ProjectData)}
	{@const Icon = projectdata.icon}

	<Glass className="w-full flex flex-col p-6 gap-6">
		<!-- Header -->
		<div class="flex gap-4 items-start">
			<div
				class="
				p-4 rounded-xl
				bg-white/10
				border border-white/15
				backdrop-blur-xl
			"
			>
				<Icon size={42} stroke-width={1.5} />
			</div>

			<div class="flex flex-col gap-2">
				<h2 class="text-2xl font-semibold">
					{projectdata.title}
				</h2>
				<p class="text-white/70 text-sm leading-relaxed max-w-prose">
					{projectdata.description}
				</p>
			</div>
		</div>

		<!-- Tags -->
		<div class="flex flex-wrap gap-2">
			{#each projectdata.tags as tag}
				<div
					class="
					px-3 py-1
					text-xs
					rounded-full
					bg-white/5
					border border-white/10
					backdrop-blur-md
					text-white/70
				"
				>
					{tag}
				</div>
			{/each}
		</div>

		<!-- <div class="flex-1"></div> -->

		<!-- Buttons -->
		<div class="flex flex-col sm:flex-row flex-wrap gap-3 mt-auto">
			<Button href={projectdata.github}>
				<Github class="w-4 h-4" />
				GitHub
			</Button>

			{#if projectdata.demo}
				<Button href={projectdata.demo} variant="secondary">
					<PanelTop class="w-4 h-4" />
					Live Demo
				</Button>
			{/if}
		</div>
	</Glass>
{/snippet}
