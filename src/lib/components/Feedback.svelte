<script lang="ts">
	import { onMount } from 'svelte';
	// import gsap from 'gsap';
	// import { ScrollTrigger } from 'gsap/ScrollTrigger';

	// gsap.registerPlugin(ScrollTrigger);

	let sectionEl: HTMLElement;
	let bgEl: HTMLElement;
	let card1: HTMLElement;
	let card2: HTMLElement;
	let card3: HTMLElement;

	let gsap: any, ScrollTrigger: any;

	onMount(async () => {
		const gsapModule = await import('gsap');
		const scrollTriggerModule = await import('gsap/ScrollTrigger');

		gsap = gsapModule.default;
		ScrollTrigger = scrollTriggerModule.default;

		gsap.registerPlugin(ScrollTrigger);

		// Create a GSAP timeline with pinned background
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: sectionEl,
				start: 'top top',
				end: '+=80%', // scroll distance
				pin: bgEl,
				scrub: true
			}
		});

		// Cards animate one by one
		tl.from(card1, {
			y: 200,

			opacity: 0,
			rotate: -8,
			duration: 1
		})
			.to(card1, { y: -10, duration: 1 }) // push up slightly when next comes
			.from(card2, {
				y: 200,
				opacity: 0,
				rotate: 6,
				duration: 1
			})
			.to([card1, card2], { y: -20, duration: 1 })
			.from(card3, {
				y: 200,
				opacity: 0,
				rotate: -4,
				duration: 1
			});
	});
</script>

<section bind:this={sectionEl} class="relative  text-white">
	<!-- Sticky / pinned background -->
	<div bind:this={bgEl} class=" relative h-full h-screen-screen w-full">
		<img
			src="https://images.prismic.io/miux-studio/aDYL_idWJ-7kSmR-_Testimonial.jpg?auto=format,compress"
			alt="Client Feedback"
			class="h-full w-full object-cover"
		/>
		<div
			class="absolute inset-0 flex flex-col items-center justify-center bg-black/50 px-4 text-center"
		>
			<h2 class="text-3xl font-bold md:text-5xl">Client Feedback</h2>
			<p class="mt-4 max-w-xl text-lg">
				Our clients share their experiences and results after working with us.
			</p>
		</div>
	</div>

	<!-- Cards container -->
	<div class="space-y-1 relative z-10 -mt-[50vh] lg:-mt-[100vh] flex flex-col items-center px-4">
		<div bind:this={card1} class="w-full max-w-3xl rounded-lg bg-white p-6 text-black shadow-lg">
			<div class="flex gap-4">
				<img
					src="https://images.prismic.io/miux-studio/aA3l0_IqRLdaBpID_client1.jpg?auto=format,compress"
					class="h-32 w-32 rounded-lg object-cover"  alt=""
				/>
				<div>
					<h3 class="text-xl font-bold">
						Jina Huang <span class="font-normal text-gray-500">CEO</span>
					</h3>
					<p class="mb-2 text-sm text-gray-500">of Watt Property Management</p>
					<p class="text-gray-600">
						“MIUX transformed our Watt Property Management website into an elegant, user-friendly
						platform...”
					</p>
				</div>
			</div>
		</div>

		<div bind:this={card2} class="w-full max-w-3xl rounded-lg bg-white p-6 text-black shadow-lg">
			<div class="flex gap-4">
				<img
					src="https://images.prismic.io/miux-studio/aA3mTvIqRLdaBpIH_client2.jpg?auto=format,compress"
					class="h-32 w-32 rounded-lg object-cover" alt=""
				/>
				<div>
					<h3 class="text-xl font-bold">
						Ana Ezpinoza <span class="font-normal text-gray-500">Co-Founder</span>
					</h3>
					<p class="mb-2 text-sm text-gray-500">Brownvase</p>
					<p class="text-gray-600">
						“Nara @ MIUX has been an exceptional designer to work with, developing our branding
						materials...”
					</p>
				</div>
			</div>
		</div>

		<div bind:this={card3} class="w-full max-w-3xl rounded-lg bg-white p-6 text-black shadow-lg">
			<div class="flex gap-4">
				<img
					src="https://images.prismic.io/miux-studio/aA3mcvIqRLdaBpIJ_client3.jpg?auto=format,compress"
					class="h-32 w-32 rounded-lg object-cover"  alt=""
				/>
				<div>
					<h3 class="text-xl font-bold">
						Hussein Saab <span class="font-normal text-gray-500">Co-Founder</span>
					</h3>
					<p class="mb-2 text-sm text-gray-500">Sparkcards</p>
					<p class="text-gray-600">
						“Nara @ MIUX is an amazing Designer! I recently gave her a tight timeline for a full
						branded UX...”
					</p>
				</div>
			</div>
		</div>
	</div>
</section>
