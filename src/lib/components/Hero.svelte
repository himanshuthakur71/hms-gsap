<script lang="ts">
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { SplitText } from 'gsap/SplitText';

	gsap.registerPlugin(SplitText);

	let heroText: any = $state(null);

	let split;

	onMount(() => {
		gsap.set(heroText, { opacity: 1 });

		SplitText.create(heroText, {
			type: 'words,lines',
			linesClass: 'line',
			autoSplit: true,
			mask: 'lines',
			onSplit: (self) => {
				split = gsap.from(self.lines, {
					duration: 0.6,
					yPercent: 100,
					opacity: 0,
					stagger: 0.1,
					ease: 'expo.out'
				});
				return split;
			}
		});

		gsap.from('#heroImg', {
			x: 700,
			duration: 0.6
		});
	});
</script>

<section class="pannel-hozi min-h-screen w-full min-w-screen bg-brand-ac-3">
	<div class="grid w-full grid-cols-1 lg:grid-cols-[1.2fr_0.8fr]">
		<div bind:this={heroText} class="split w-full px-8 pt-32 pb-8">
			<p class=" mb-4 text-5xl">
				Hi, I’m <span class=" font-semibold text-amber-600">Himanshu Thakur</span>
			</p>
			<p class=" mb-2 text-xl font-light">
				Building sleek, performant, and user-friendly apps with a creative twist.
			</p>
			<p class=" text-xl font-light">
				From clean UI animations to rock-solid backend logic, I turn ideas into smooth, functional
				experiences.
			</p>

			<div class="mt-8 w-full text-lg font-light">
				<p>
					I’m a front-end and full-stack developer passionate about building modern,
					high-performance web applications. My expertise lies in SvelteKit, TypeScript, Tailwind
					CSS, Supabase, and serverless architectures, with a strong focus on performance,
					accessibility, and clean design.
				</p>

				<p class="mt-2">
					I love combining beautiful UI animations with robust data-driven features — whether it’s
					creating scroll-driven motion effects, custom dashboards, or interactive 3D experiences.
				</p>
			</div>

			<div class="mt-6 w-full">
				<button
					type="button"
					class="flex h-[42px] cursor-pointer items-center justify-center rounded-[5px] bg-brand-ac-4 px-4 text-white hover:opacity-80"
					>Download Resume</button
				>
			</div>
		</div>
		<div class="relative z-[10] flex h-full w-full items-center justify-center">
			<figure class=" flex h-full w-full items-center justify-center" id="heroImg">
				<img src="/images/mani.JPG" alt="user" class="h-full min-h-screen w-full object-cover" />
			</figure>
		</div>
	</div>
</section>

<style>
	.split * {
		will-change: transform;
	}
</style>
