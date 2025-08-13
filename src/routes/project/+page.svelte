<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import gsap from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';

	gsap.registerPlugin(ScrollTrigger);

	let headingEl: HTMLHeadingElement;
	let paraEl: HTMLParagraphElement;

	onMount(() => {
		// ==== Heading Split & Animation ====
		const chars = headingEl.textContent?.split('') ?? [];
		headingEl.innerHTML = chars
			.map(
				(char) =>
					`<span class="overflow-hidden inline-block">
						<span class="inner inline-block translate-y-full">${char}</span>
					</span>`
			)
			.join('');

		const innerEls = headingEl.querySelectorAll<HTMLElement>('.inner');

		gsap.to(innerEls, {
			y: 0,
			duration: 1,
			stagger: 0.05,
			ease: 'power3.out',
			scrollTrigger: {
				trigger: headingEl,
				start: 'top 80%',
			}
		});

		// ==== Paragraph: Line-by-Line Animation ====
		const lines = splitIntoLines(paraEl);
		gsap.from(lines, {
			yPercent: 100,
			duration: 0.8,
			stagger: 0.15,
			ease: 'power3.out',
			scrollTrigger: {
				trigger: paraEl,
				start: 'top 85%',
			}
		});
	});

	onDestroy(() => {
		ScrollTrigger.getAll().forEach((t) => t.kill());
	});

	// Utility to wrap each visual line in spans
	function splitIntoLines(element: HTMLElement) {
		const text = element.innerHTML;
		element.innerHTML = '';

		// We create a temp div to measure
		const words = text.split(' ');
		let currentLine: HTMLElement | null = null;
		let lines: HTMLElement[] = [];

		words.forEach((word, i) => {
			if (!currentLine) {
				currentLine = document.createElement('div');
				currentLine.className = 'overflow-hidden leading-relaxed';
				element.appendChild(currentLine);
				lines.push(currentLine);
			}
			const testSpan = document.createElement('span');
			testSpan.textContent = (i > 0 ? ' ' : '') + word;
			currentLine.appendChild(testSpan);

			// Check if this span caused a line break
			if (currentLine.offsetHeight > testSpan.offsetHeight * 1.5) {
				// New line
				currentLine.removeChild(testSpan);
				currentLine = document.createElement('div');
				currentLine.className = 'overflow-hidden leading-relaxed';
				element.appendChild(currentLine);
				currentLine.appendChild(testSpan);
				lines.push(currentLine);
			}
		});

		// Wrap inner text in a span for animation
		lines.forEach((line) => {
			const inner = document.createElement('span');
			inner.className = 'block';
			inner.innerHTML = line.innerHTML;
			line.innerHTML = '';
			line.appendChild(inner);
		});

		return element.querySelectorAll('div > span');
	}
</script>

<svelte:head>
	<title>Projects | HMS</title>
</svelte:head>

<section class="w-full">
	<div class="px-4">
		<section class="pt-32 w-full">
			<h1 bind:this={headingEl} class="text-[256px] font-bold leading-none">
				Work
			</h1>
			<p bind:this={paraEl} class="max-w-3xl mt-8 text-lg leading-relaxed">
				Lorem ipsum dolor sit amet consectetur, adipisicing elit. Rerum suscipit officiis temporibus non explicabo in aliquid maiores ab nam quos architecto, voluptates nisi enim quod natus, asperiores culpa dolorem dignissimos. Perferendis, laborum, numquam ducimus repudiandae incidunt aliquid praesentium tempore autem quam consequuntur neque reiciendis iste?
			</p>
		</section>
	</div>
</section>

<style>
	.inner {
		display: inline-block;
	}
</style>
