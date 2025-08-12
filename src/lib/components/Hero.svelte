<script>
	import { onMount } from 'svelte';
	import { gsap } from 'gsap';

	onMount(() => {
		gsap.from('.hero-content', {
			opacity: 0,
			y: 50,
			duration: 1,
			ease: 'power3.out',
			scrollTrigger: {
				trigger: '.hero',
				start: 'top center',
				toggleActions: 'play none none reverse'
			}
		});
	});
</script>

<section class="min-h-screen w-full min-w-screen !bg-[#d5c8b0] panel">
	<div class="grid w-full grid-cols-[1.2fr_0.8fr]">
		<div class="w-full pt-32 pb-8 px-8">
			<p class=" mb-4 text-5xl">
				Hi, I’m <span class=" font-semibold text-amber-600">Himanshu Thakur</span>
			</p>
			<p class=" text-xl mb-2  font-light">
				Building sleek, performant, and user-friendly apps with a creative twist.
			</p>
			<p class=" text-xl font-light">
				From clean UI animations to rock-solid backend logic, I turn ideas into smooth, functional
				experiences.
			</p>

            <div class="w-full  text-lg font-light mt-8">
                <p>I’m a front-end and full-stack developer passionate about building modern, high-performance web applications. My expertise lies in SvelteKit, TypeScript, Tailwind CSS, Supabase, and serverless architectures, with a strong focus on performance, accessibility, and clean design.</p>

                <p class="mt-2">I love combining beautiful UI animations with robust data-driven features — whether it’s creating scroll-driven motion effects, custom dashboards, or interactive 3D experiences.</p>
            </div>
		</div>
		<div class="relative z-[10] flex h-full w-full items-center justify-center">
			<figure class=" flex w-full h-full justify-center items-center">
                <img src="/images/mani.JPG" alt="user" class="h-full w-full min-h-screen object-cover" />
            </figure>
		</div>
	</div>
</section>
