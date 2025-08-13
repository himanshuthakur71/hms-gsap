<script lang="ts">
	import { onMount } from 'svelte';
	import gsap from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';

	gsap.registerPlugin(ScrollTrigger);

	let sectionEl: HTMLElement;
	let bgEl: HTMLElement;
	let card1: HTMLElement;
	let card2: HTMLElement;
	let card3: HTMLElement;

	onMount(() => {
		// Create a GSAP timeline with pinned background
		const tl = gsap.timeline({
			scrollTrigger: {
				trigger: sectionEl,
				start: "top top",
				end: "+=70%", // scroll distance
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

<section bind:this={sectionEl} class="relative bg-neutral-900 text-white">
	<!-- Sticky / pinned background -->
	<div bind:this={bgEl} class=" h-full  min-h-screen w-full relative">
		<img 
			src="https://images.prismic.io/miux-studio/aDYL_idWJ-7kSmR-_Testimonial.jpg?auto=format,compress"
			alt="Client Feedback"
			class="h-full w-full object-cover"
		/>
		<div class="absolute inset-0 bg-black/50 flex flex-col items-center justify-center text-center px-4">
			<h2 class="text-3xl md:text-5xl font-bold">Client Feedback</h2>
			<p class="max-w-xl mt-4 text-lg">Our clients share their experiences and results after working with us.</p>
		</div>
	</div>

	<!-- Cards container -->
	<div class="relative z-10 -mt-[80vh] flex flex-col items-center space-y-">
		<div bind:this={card1} class="max-w-3xl w-full bg-white text-black rounded-lg shadow-lg p-6">
			<div class="flex gap-4">
				<img src="https://images.prismic.io/miux-studio/aA3l0_IqRLdaBpID_client1.jpg?auto=format,compress" class="w-32 h-32 object-cover rounded-lg" />
				<div>
					<h3 class="font-bold text-xl">Jina Huang <span class="text-gray-500 font-normal">CEO</span></h3>
					<p class="text-gray-500 text-sm mb-2">of Watt Property Management</p>
					<p class="text-gray-600">“MIUX transformed our Watt Property Management website into an elegant, user-friendly platform...”</p>
				</div>
			</div>
		</div>

		<div bind:this={card2} class="max-w-3xl w-full bg-white text-black rounded-lg shadow-lg p-6">
			<div class="flex gap-4">
				<img src="https://images.prismic.io/miux-studio/aA3mTvIqRLdaBpIH_client2.jpg?auto=format,compress" class="w-32 h-32 object-cover rounded-lg" />
				<div>
					<h3 class="font-bold text-xl">Ana Ezpinoza <span class="text-gray-500 font-normal">Co-Founder</span></h3>
					<p class="text-gray-500 text-sm mb-2">Brownvase</p>
					<p class="text-gray-600">“Nara @ MIUX has been an exceptional designer to work with, developing our branding materials...”</p>
				</div>
			</div>
		</div>

		<div bind:this={card3} class="max-w-3xl w-full bg-white text-black rounded-lg shadow-lg p-6">
			<div class="flex gap-4">
				<img src="https://images.prismic.io/miux-studio/aA3mcvIqRLdaBpIJ_client3.jpg?auto=format,compress" class="w-32 h-32 object-cover rounded-lg" />
				<div>
					<h3 class="font-bold text-xl">Hussein Saab <span class="text-gray-500 font-normal">Co-Founder</span></h3>
					<p class="text-gray-500 text-sm mb-2">Sparkcards</p>
					<p class="text-gray-600">“Nara @ MIUX is an amazing Designer! I recently gave her a tight timeline for a full branded UX...”</p>
				</div>
			</div>
		</div>
	</div>
</section>


