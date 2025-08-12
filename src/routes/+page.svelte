<script lang="ts">
	import Hero from '$lib/components/Hero.svelte';
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';
	import Info from '$lib/components/Info.svelte';
	import Prallex from '$lib/components/Prallex.svelte';
	import ExperinceSection from '$lib/components/ExperinceSection.svelte';

	gsap.registerPlugin(ScrollTrigger);

    let horizontalSection: any = $state(null);

	onMount(() => {
		const container:any = horizontalSection;
		const panels:any = gsap.utils.toArray('.panel');

		// Horizontal scroll effect
		gsap.to(panels, {
			xPercent: -100 * (panels.length - 1),
			ease: 'none',
			scrollTrigger: {
				trigger: container,
				pin: true,
				scrub: 1,
				snap: 1 / (panels.length - 1),
				end: () => '+=' + container.offsetWidth
			}
		});
	});
</script>

<!-- Horizontal scroll section -->
<section bind:this={horizontalSection} class="horizontal-section flex w-full">
	<Hero />
	<Info />
</section>

<!-- Normal scroll section -->
<Prallex />
<ExperinceSection />


