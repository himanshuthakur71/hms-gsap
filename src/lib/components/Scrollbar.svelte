<script lang="ts">
	// import gsap from "gsap";
	// import ScrollTrigger from "gsap/ScrollTrigger";
	import { onMount } from 'svelte';

	// gsap.registerPlugin(ScrollTrigger);

	let gsap: any, ScrollTrigger: any;

	onMount(async () => {
		const gsapModule = await import('gsap');
		const scrollTriggerModule = await import('gsap/ScrollTrigger');

		gsap = gsapModule.default;
		ScrollTrigger = scrollTriggerModule.default;

		gsap.registerPlugin(ScrollTrigger);

		const scrollbar = document.getElementById('scroolbar');

		if (!scrollbar) return;

		gsap.to(scrollbar, {
			width: '100%',
			ease: 'none',
			scrollTrigger: {
				trigger: document.body, // the whole page
				start: 'top top',
				end: 'bottom bottom',
				scrub: true
			}
		});
	});
</script>

<!-- Progress bar -->
<div id="scroolbar" class="absolute top-[72px] left-0 h-[1px] w-0 bg-brand-dark"></div>
