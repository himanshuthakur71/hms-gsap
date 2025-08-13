<script>
	import gsap from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	import { onMount } from 'svelte';

	gsap.registerPlugin(ScrollTrigger);

	onMount(() => {
		// Parallax background
		gsap.to('#cta-bg', {
			yPercent: -20,
			ease: 'none',
			scrollTrigger: {
				trigger: '#cta-bg',
				start: 'top bottom',
				scrub: true
			}
		});

		// Text reveal animations
		gsap.fromTo(
			'#cta-subtitle',
			{ y: 30, opacity: 0 },
			{ y: 0, opacity: 1, duration: 1, delay: 0.2 }
		);
		gsap.fromTo('#cta-title', { y: 50, opacity: 0 }, { y: 0, opacity: 1, duration: 1, delay: 0.6 });
		gsap.fromTo('#cta-button', { y: 40, opacity: 0 }, { y: 0, opacity: 1, duration: 1, delay: 1 });
	});
</script>

<section class="relative flex h-screen items-center justify-center overflow-hidden">
	<!-- Background -->
	<div class="absolute inset-0 overflow-hidden">
		<img
			src="https://images.prismic.io/miux-studio/aA-uEfIqRLdaBrm9_cta-section-background.png?auto=format,compress"
			alt="bg"
			class="h-full w-full object-cover will-change-transform"
			id="cta-bg"
		/>
	</div>

	<!-- Overlay for readability -->
	<div class="absolute inset-0 bg-black/40"></div>

	<!-- Content -->
	<div class="relative z-10 mx-auto max-w-5xl px-6 text-center text-white">
		<p class="mb-4 text-lg opacity-0 md:text-xl" id="cta-subtitle">
			Contact us today to discuss your project and get a tailored quote.
		</p>

		<h1 class="text-5xl leading-tight font-bold opacity-0 md:text-7xl" id="cta-title">
			Let’s bring your vision to life.
		</h1>

		<a
			href="/contact"
			class="mt-8 inline-flex items-center gap-3 rounded-full bg-white px-6 py-3 font-semibold text-black opacity-0 shadow-lg transition-opacity hover:bg-gray-200"
			id="cta-button"
		>
			Inquire
			<svg width="20" height="20" fill="currentColor" viewBox="0 0 17 16">
				<path
					d="M8.53 15.67L7.47 14.61 13.26 8.82H0.93V7.32H13.26L7.47 1.53 8.53 0.47 16.13 8.07 8.53 15.67Z"
				></path>
			</svg>
		</a>
	</div>
</section>
