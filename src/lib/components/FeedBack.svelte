<script lang="ts">
	import { onMount } from 'svelte';
	import gsap from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';

	gsap.registerPlugin(ScrollTrigger);

	let cards: HTMLDivElement[] = [];

	const cardData = [
		{ rotate: 5 },
		{ rotate: -8 },
		{ rotate: 3 }
	];

	onMount(() => {
		cards.forEach((card, i) => {
			gsap.set(card, {
				rotation: cardData[i].rotate,
				y: i * 2, // tiny offset so they aren't pixel-perfect
				zIndex: cardData.length - i
			});
		});

		// Animate each card away on scroll
		cards.forEach((card, i) => {
			if (i === cards.length - 1) return; // last card stays

			gsap.to(card, {
				y: '-120%',
				rotation: cardData[i].rotate + gsap.utils.random(-10, 10),
				opacity: 0,
				scrollTrigger: {
					trigger: card,
					start: 'top center+=100',
					end: 'bottom center',
					scrub: true
				}
			});
		});
	});
</script>

<div class="relative flex  min-h-[calc(100vh*2)] items-center justify-center bg-gray-100">
	<div class="relative w-full max-w-[500px] h-[640px]">
		{#each cardData as { rotate }, i}
			<div
				bind:this={cards[i]}
				class="absolute top-0 left-0 h-full w-full rounded bg-[#f7f3ed] p-2 shadow-lg"
			>
				<figure class="flex h-[325px] w-full overflow-hidden rounded">
					<img
						src="https://madeinuxstudio.com/_next/image?url=https%3A%2F%2Fimages.prismic.io%2Fmiux-studio%2FaA3mcvIqRLdaBpIJ_client3.jpg%3Fauto%3Dformat%2Ccompress&w=1080&q=90"
						alt=""
						class="h-full w-full object-cover"
					/>
				</figure>
				<div class="p-4">
					<p class="text-center">xxFullNamexx <span></span> xxTitlexx</p>
					<p class="text-center">xxBrandxx</p>

					<figure class="mx-auto flex h-[72px] w-[167px] items-center justify-center">
						<img
							src="https://miux-studio.cdn.prismic.io/miux-studio/aA_QuPIqRLdaBrw2_sign-about-3.svg"
							alt=""
							class="h-full w-full"
						/>
					</figure>

					<p>
						Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ab tempore consectetur ut suscipit
						libero eos natus asperiores in molestiae distinctio, sit accusantium quaerat repudiandae
						aliquam, placeat cupiditate deleniti earum sequi nisi. Voluptatem!
					</p>
				</div>
			</div>
		{/each}
	</div>
</div>
