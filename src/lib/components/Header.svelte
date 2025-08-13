<script lang="ts">
	import gsap from 'gsap';
	import { onDestroy, onMount } from 'svelte';

	let tl001: any = $state(null);

	onMount(() => {


		tl001 = gsap.timeline();

		tl001.to('.text-001 span', {
			y: -25,
			duration: 0.3,
			stagger: 0.1 // small delay for second span
		});

		tl001.to('.icon-001 svg', {
			y: -13,
			duration: 0.3,
			stagger: 0.1 // small delay for second span
		});

		tl001.pause();
	});


	onDestroy(() => {
		tl001 = null
	})
</script>


<header
	class="fixed top-0 left-0 z-[999] flex h-[72px] w-full items-center justify-between border-b border-[#0000001a]"
>
	<div class="flex h-full items-center">
		<a
			href="/"
			aria-label="home"
			class="flex h-full w-[130px] items-center justify-center border-r border-[#0000001a]"
		>
			<img src="/images/signature.svg" alt="" class=" h-[40px] w-[130px]" />
		</a>
		<div class="w-full max-w-[280px] px-4">
			<p class=" line-clamp-[115%] text-[11px] text-[#333335]">
				Crafting sleek, high-performance web experiences with code and creativity.
			</p>
		</div>
	</div>

	<div class="flex h-full items-center">

		<a
			href="/project"
			class="flex w-[146.4px] flex-col justify-between border-l border-dark-10 p-4"
			onmouseenter={() => tl001.play()}
			onmouseleave={() => tl001.reverse()}
		>
			<span class="text-[11.2px] leading-[12.88px]">Projects</span>
			<div class="flex items-center justify-between">
				<!-- Text -->
				<p class="text-001 grid h-[16.4px] overflow-hidden text-[14.4px]">
					<span class="inline-block">Work</span>
					<span class="inline-block">Work</span>
				</p>

				<!-- Icon -->
				<div class="icon-001 grid h-[13px] w-[13px] overflow-hidden text-brand-dark">
					<svg
						class="shrink-0"
						id="f1"
						xmlns="http://www.w3.org/2000/svg"
						width="13"
						height="13"
						fill="none"
						viewBox="0 0 13 13"
					>
						<path
							stroke="currentColor"
							stroke-width="1.5"
							d="m5.677 1 5.657 5.657m0 0-5.657 5.657m5.657-5.657H.02"
						></path>
					</svg>
					<svg
						class="shrink-0"
						id="f2"
						xmlns="http://www.w3.org/2000/svg"
						width="13"
						height="13"
						fill="none"
						viewBox="0 0 13 13"
					>
						<path
							stroke="currentColor"
							stroke-width="1.5"
							d="m5.677 1 5.657 5.657m0 0-5.657 5.657m5.657-5.657H.02"
						></path>
					</svg>
				</div>
			</div>
		</a>
	</div>
</header>
