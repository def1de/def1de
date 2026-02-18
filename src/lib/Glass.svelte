<script lang="ts">
	let { className = '', children } = $props();

	type Blob = {
		size: number;
		x: number;
		y: number;
		color: string;
		opacity: number;
	};

	function createBlob(): Blob {
		return {
			size: 40 + Math.random() * 60, // % of container
			x: Math.random() * 100,
			y: Math.random() * 100,
			color: ['bg-purple-500', 'bg-cyan-400', 'bg-blue-500'][Math.floor(Math.random() * 3)],
			opacity: 0.2 + Math.random() * 0.3
		};
	}

	// Generate once
	const blobs: Blob[] = Array.from({ length: 3 }, createBlob);
</script>

<div class={`relative isolate`}>
	<!-- Content Wrapper -->
	<div class={`w-full h-full relative z-10 flex items-center justify-center`}>
		<div
			class={`w-full h-full rounded-2xl 
			bg-white/5 
			backdrop-blur-2xl 
			border border-white/10 
			shadow-[0_0_60px_rgba(0,0,0,0.6)]
            overflow-hidden`}
		>
			<div class="absolute inset-0 -z-10 h-full">
				{#each blobs as blob}
					<div
						class={`absolute rounded-full blur-[120px] ${blob.color}`}
						style="
							width: {blob.size}%;
							height: {blob.size}%;
							left: {blob.x}%;
							top: {blob.y}%;
							opacity: {blob.opacity};
							transform: translate(-50%, -50%);
						"
					></div>
				{/each}
			</div>
			<div class={`relative z-10 h-full ${className}`}>
				{@render children()}
			</div>
		</div>
	</div>
</div>

<style>
	@keyframes float {
		0% {
			transform: translate(-50%, -50%) translateY(0px);
		}
		50% {
			transform: translate(-50%, -50%) translateY(-10px);
		}
		100% {
			transform: translate(-50%, -50%) translateY(0px);
		}
	}
</style>
