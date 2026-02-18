<script lang="ts">
	import Glass from '$lib/Glass.svelte';
	import '@fortawesome/fontawesome-free/css/all.min.css';
	import { Code, PanelsTopLeft } from '@lucide/svelte';

	type SubskillData = {
		icon: string;
		title: string;
	};
	type SkillData = {
		icon: typeof Code;
		title: string;
		subskills: SubskillData[];
	};

	let skills: SkillData[] = [
		{
			icon: Code,
			title: 'Languages',
			subskills: [
				{
					icon: 'fa-brands fa-python',
					title: 'Python'
				},
				{
					icon: 'fa-brands fa-rust',
					title: 'Rust'
				},
				{
					icon: 'fa-solid fa-c',
					title: 'C/C++'
				},
				{
					icon: 'fa-brands fa-java',
					title: 'Java'
				}
			]
		},
		{
			icon: PanelsTopLeft,
			title: 'Frameworks',
			subskills: [
				{
					icon: 'fa-brands fa-svelte',
					title: 'Svelte'
				},
				{
					icon: 'fa-solid fa-tower-cell',
					title: 'Axum'
				},
				{
					icon: 'fa-solid fa-flask',
					title: 'Flask'
				},
				{
					icon: 'fa-solid fa-gamepad',
					title: 'SFML'
				}
			]
		}
	];
</script>

<section class="w-full flex-1 mb-3">
	<!-- Section Header -->
	<div class="mb-6">
		<h2 class="text-2xl font-bold text-surface-50 mb-2">Technical Skills</h2>
		<p class="text-sm text-surface-400">Languages and frameworks I am using</p>
	</div>

	<div class="grid grid-cols-1 gap-3 md:grid-cols-2">
		{#each skills as skilldata}
			{@render skill(skilldata)}
		{/each}
	</div>
</section>

{#snippet skill(skill: SkillData)}
	{@const Icon = skill.icon}

	<Glass className="w-full flex flex-col p-6 gap-6">
		<!-- Header -->
		<div class="flex items-center gap-4">
			<div
				class="
				p-3 rounded-xl
				bg-white/10
				border border-white/15
				backdrop-blur-xl
			"
			>
				<Icon size={28} stroke-width={1.5} />
			</div>

			<h2 class="text-2xl font-semibold tracking-tight">
				{skill.title}
			</h2>
		</div>

		<!-- Subskills -->
		<div class="grid grid-cols-2 sm:grid-cols-3 gap-3">
			{#each skill.subskills as sub}
				{@render subskill(sub.icon, sub.title)}
			{/each}
		</div>
	</Glass>
{/snippet}

{#snippet subskill(icon: string, text: string)}
	<div
		class="
		flex items-center justify-center gap-2
		px-4 py-2
		rounded-xl
		bg-white/5
		border border-white/10
		backdrop-blur-md
		hover:bg-white/10
		transition-all duration-200
	"
	>
		<i class={`${icon} text-xl opacity-80`}></i>
		<span class="text-sm opacity-80">{text}</span>
	</div>
{/snippet}
