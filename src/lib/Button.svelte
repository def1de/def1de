<script lang="ts">
	let { href = '#', children, variant = 'primary' } = $props();
</script>

<a
	{href}
	target="_blank"
	class={`
		w-full
		inline-flex items-center justify-center gap-2
		px-5 py-2.5
		rounded-xl
		text-sm font-medium text-nowrap
		transition-all duration-200
		backdrop-blur-md
		border
		mb-3
		${
			variant === 'primary'
				? `
			bg-white/10 
			border-white/20 
			hover:bg-white/20 
			hover:shadow-[0_0_20px_rgba(139,92,246,0.4)]
			`
				: `
			bg-white/5 
			border-white/10 
			hover:bg-white/10
			`
		}
	`}
>
	{@render children()}
</a>
