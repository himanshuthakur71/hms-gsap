<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import gsap from 'gsap';
	import ScrollTrigger from 'gsap/ScrollTrigger';

	gsap.registerPlugin(ScrollTrigger);

	let sectionE5: HTMLElement;
	let tl5: gsap.core.Timeline;

	onMount(() => {
		tl5 = gsap.timeline({
			scrollTrigger: {
				trigger: sectionE5,
				start: 'top 100%', // when top of section hits 80% viewport
				toggleActions: 'restart none restart none', // always run in both directions
				markers: true // uncomment for debugging
			}
		});

		tl5
			.from(sectionE5.querySelectorAll('li'), {
				x: -50,
				opacity: 0,
				duration: 0.6,
				stagger: 0.15,
				ease: 'power3.out'
			})
			.from(
				sectionE5.querySelector('h3'),
				{
					x: 50,
					opacity: 0,
					duration: 0.8,
					ease: 'power3.out'
				},
				'-=0.3'
			)
			.from(
				sectionE5.querySelector('p'),
				{
					y: 20,
					opacity: 0,
					duration: 0.6,
					ease: 'power2.out'
				},
				'-=0.4'
			)

            .from(
				sectionE5.querySelector('.p2'),
				{
					y: 20,
					opacity: 0,
					duration: 0.6,
					ease: 'power2.out'
				},
				'-=0.4'
			);
	});

	onDestroy(() => {
		if (tl5) tl5.kill();
		ScrollTrigger.getAll().forEach((st) => st.kill());
	});
</script>

<section bind:this={sectionE5} class="h-full w-full bg-[#f7f3ed] py-38">
	<div class="grid w-full grid-cols-2 gap-8 px-4">
		<div class="w-full">
			<ul class="w-full max-w-[355px]">
				{#each Array(4) as _, i}
					<li
						class="flex items-center gap-4 border-t border-[#0000001a] py-2"
						class:border-b={i === 3}
					>
						<span
							class="flex size-[25px] items-center justify-center rounded-full bg-[#d5c8b0] text-[11px]"
							>{i + 1}</span
						>
						<span class="text-[22px] font-[400] text-[#333335]">Lorem ipsum dolor sit.</span>
					</li>
				{/each}
			</ul>
		</div>

		<div class="w-full">
			<p class="flex items-center gap-4 text-[14px] text-[#9e8f7b]">
				<span class="flex size-[5px] items-center justify-center rounded-full bg-[#9e8f7b]"></span>
				From idea to impact
			</p>

			<h3 class="mt-4 text-[51px] leading-[51px]">
				<span class="block">Lorem ipsum dolor sit</span>
				<span class="block"> amet consectetur</span>
			</h3>

			<p class="mt-8 max-w-[356px] text-[16px] text-[#00000080] p2">
				Lorem ipsum dolor sit amet consectetur adipisicing elit. Dolores quod, distinctio possimus
				repellat pariatur facere similique? Deleniti aliquid pariatur, voluptate labore enim in,
				officia earum totam quia odio iste id recusandae hic!
			</p>
		</div>
	</div>
</section>
