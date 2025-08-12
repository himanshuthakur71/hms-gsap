<script lang="ts">
	import { onMount } from 'svelte';
	import gsap from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';

	gsap.registerPlugin(ScrollTrigger);

	let cards: HTMLDivElement[] = [];

	onMount(() => {
		cards.forEach((card, i) => {
			ScrollTrigger.create({
				trigger: card,
				start: 'top center',
				end: '+=200%',
				pin: true,
				pinSpacing: false,
				onEnter: () => gsap.to(card, { autoAlpha: 1, y: 0, duration: 0.6 }),
				onLeaveBack: () => gsap.to(card, { autoAlpha: 0, y: 50, duration: 0.4 })
			});
		});
	});
</script>

<section class="relative min-h-screen w-ful">
	
		<div
			class="absolute inset-0 bg-cover bg-fixed bg-center"
			style={`background-image: url(https://madeinuxstudio.com/_next/image?url=https%3A%2F%2Fimages.prismic.io%2Fmiux-studio%2FaDYL_idWJ-7kSmR-_Testimonial.jpg%3Fauto%3Dformat%2Ccompress&w=1920&q=90`}
		></div>

		<div class="mx-auto flex max-w-3xl flex-col items-center">
			{#each [{ rotate: 'rotate-2' }, { rotate: '-rotate-2' }, { rotate: 'rotate-1' }] as { rotate }, i}
				<div
					bind:this={cards[i]}
					class={`sticky top-20 my-10 w-full max-w-xl translate-y-12 transform rounded-xl bg-white p-4 opacity-0 shadow-lg ${rotate}`}
				>
					<figure class="h-64 w-full overflow-hidden rounded-lg">
						<img
							src="https://picsum.photos/600/400?random={i}"
							alt=""
							class="h-full w-full object-cover"
						/>
					</figure>
					<div class="mt-4 space-y-2">
						<p class="text-center text-lg font-bold">Full Name {i + 1}</p>
						<p class="text-center text-sm text-gray-500">Brand / Role</p>
						<p class="text-gray-700">
							Lorem ipsum dolor sit amet, consectetur adipisicing elit. Eos incidunt beatae ullam
							reiciendis soluta quae expedita pariatur suscipit tempora nostrum!
						</p>
					</div>
				</div>
			{/each}
		</div>
	
</section>
