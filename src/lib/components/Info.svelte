<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import gsap from 'gsap';
	import ScrollTrigger from 'gsap/ScrollTrigger';

	gsap.registerPlugin(ScrollTrigger);

	let sectionEl: HTMLElement;
	let tl: gsap.core.Timeline | undefined;

	onMount(() => {
		if (!sectionEl) return;

		// Select elements to animate
		const textItems = sectionEl.querySelectorAll<HTMLElement>('.animate-item');
		const cards = sectionEl.querySelectorAll<HTMLElement>('.animate-card');

		// initial set (so elements are ready before the ScrollTrigger fires)
		gsap.set(textItems, { y: 40, opacity: 0 });
		gsap.set(cards, { y: 60, opacity: 0, scale: 0.98 });

		// timeline with ScrollTrigger — runs when section enters viewport
		tl = gsap.timeline({
			scrollTrigger: {
				trigger: sectionEl,
				start: 'top 80%',           // tweak to your taste
				toggleActions: 'play none none reverse',
				// markers: true,          // uncomment for debugging
			}
		});

		// stagger text items first
		tl.to(textItems, {
			y: 0,
			opacity: 1,
			duration: 0.7,
			stagger: 0.12,
			ease: 'power3.out'
		});

		// then animate the 3 cards with a little overlap
		tl.to(cards, {
			y: 0,
			opacity: 1,
			scale: 1,
			duration: 0.8,
			stagger: 0.12,
			ease: 'power3.out'
		}, '-=0.25');
	});

	onDestroy(() => {
		if (tl) tl.kill();
		ScrollTrigger.getAll().forEach(st => st.kill());
	});
</script>


<section  bind:this={sectionEl} class="panel relative min-h-[calc(100vh_72px)] w-full min-w-screen !bg-[#f7f3ed] animate-section">
	<div class="grid h-full w-full grid-cols-[0.8fr_1.2fr]">
		<div class="max-h-[calc(100vh_72px)] w-full overflow-hidden px-8 pt-32 pr-6 pb-8 text-black">
			<h2 class="animate-item mb-4 text-4xl font-semibold">About Me</h2>

			<p class="animate-item mb-2 text-xl font-light">
				I’m a front-end and full-stack developer passionate about building modern, high-performance
				web applications that balance elegant design with technical excellence. My expertise spans
				SvelteKit, TypeScript, Tailwind CSS, Supabase, and serverless architectures, with a sharp
				focus on performance, accessibility, and maintainable code.
			</p>

			<p class="animate-item mb-2 text-xl font-light">
				I specialize in crafting beautiful, interactive UI animations and pairing them with robust,
				data-driven features — from scroll-driven motion effects and dynamic dashboards to immersive
				3D experiences.
			</p>

			<p class="animate-item mb-2 text-xl font-light">
				Beyond traditional web development, I have hands-on experience with AI and LLM integration,
				including building voice and video AI agent models capable of real-time interaction,
				transcription, and intelligent responses. I enjoy designing systems that merge natural
				language understanding, machine learning APIs, and custom automation workflows to create
				smarter, more adaptive applications.
			</p>

			<p class="animate-item text-xl font-light">
				Whether it’s designing a health data dashboard with AI-powered PDF parsing, developing
				voice-driven interfaces, or building scroll-driven cinematic animations, I bring creativity
				and precision to every project — ensuring the end product is fast, engaging, and built to
				last.
			</p>
		</div>

		<div class="h-full w-full">
			<div class=" grid h-full w-full grid-cols-3 pt-[72px]">
				<div
					class=" animate-card group relative h-full w-full border-l border-[#0000001a] text-black transition-all duration-300 hover:text-white"
				>
					<img
						src="/images/aFzHU3fc4bHWivEC_Home_hero_1.avif"
						alt=""
						class="absolute inset-0 h-full w-full object-cover opacity-0 transition-opacity duration-500 group-hover:opacity-100"
					/>
					<div class="relative px-4">
						<span class=" block text-[320px] font-bold">1</span>
						<p class=" text-4xl leading-10 font-semibold">UX/UI <br />Design</p>
						<p class="mt-4 font-extralight">
							Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae ipsum soluta aliquam.
						</p>
					</div>
				</div>
				<div
					class="animate-card group relative h-full w-full border-l border-[#0000001a] text-black transition-all duration-300 hover:text-white"
				>
					<img
						src="/images/aFzHU3fc4bHWivEC_Home_hero_1.avif"
						alt=""
						class="absolute inset-0 h-full w-full object-cover opacity-0 transition-opacity duration-500 group-hover:opacity-100"
					/>
					<div class="relative px-4">
						<span class="block text-[320px] font-bold">2</span>
						<p class="text-4xl leading-10 font-semibold">
							Dashboard<br />Design
						</p>
						<p class="mt-4 font-extralight">
							Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae ipsum soluta aliquam.
						</p>
					</div>
				</div>

				<div
					class="animate-card group relative h-full w-full border-l border-[#0000001a] text-black transition-all duration-300 hover:text-white"
				>
					<img
						src="/images/aFzHU3fc4bHWivEC_Home_hero_1.avif"
						alt=""
						class="absolute inset-0 h-full w-full object-cover opacity-0 transition-opacity duration-500 group-hover:opacity-100"
					/>
					<div class="relative px-4">
						<span class=" block text-[320px] font-bold">3</span>
						<p class=" text-4xl leading-10 font-semibold">Website<br />Design</p>
						<p class="mt-4 font-extralight">
							Lorem ipsum dolor sit amet consectetur, adipisicing elit. Beatae ipsum soluta aliquam.
						</p>
					</div>
				</div>
			</div>
		</div>
	</div>
</section>
