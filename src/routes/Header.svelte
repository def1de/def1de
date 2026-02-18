<script lang="ts">
	import { HyperText } from '$lib/components/magic/hyper-text';
	import { DotPattern } from '$lib/components/magic/dot-pattern';
	import { cn } from '$lib/utils';

	import Button from '$lib/Button.svelte';
	import pfp from '$lib/assets/profile_picture.jpg';
	import { Github, Instagram } from '@lucide/svelte';
</script>

<section class="w-full flex flex-col gap-2 mb-3">
	<div class="w-full bg-black relative flex flex-col items-center justify-center">
		<DotPattern
			class={`${cn('mask-[radial-gradient(1000px_circle_at_center,white,transparent)]')}`}
			cr={1}
		/>
		<!-- svelte-ignore a11y_img_redundant_alt -->
		<div class="z-10 py-6 flex flex-col md:flex-row">
			<div class="w-full flex flex-col justify-center items-center mb-5">
				<img src={pfp} alt="profile picture" class="rounded-full w-40 object-cover mt-16 mb-5" />
				<HyperText class="text-xl" duration={1000} text="Illia Katerynych"></HyperText>
			</div>
			<div class="w-full flex flex-col justify-center items-center mb-5 px-8">
				<Button href="https://github.com/def1de">
					<Github class="w-5 h-5 mr-2" />
					View on GitHub
				</Button>
				<Button href="https://www.instagram.com/iktrnch/">
					<Instagram class="w-5 h-5 mr-2" />
					Follow on Instagram
				</Button>
			</div>
		</div>
	</div>
</section>
