<script lang="ts">
	import { onMount, onDestroy } from 'svelte';
	import { goto } from '$app/navigation';
	import gsap from 'gsap';
	import { ScrollTrigger } from 'gsap/ScrollTrigger';

	gsap.registerPlugin(ScrollTrigger);

	let headingEl: HTMLHeadingElement;
	let paraEl: HTMLParagraphElement;

	const projects = [
		{ id: 1, title: 'Project One', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.', projectImage: 'https://picsum.photos/600/400?random=1' },
		{ id: 2, title: 'Project Two', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.', projectImage: 'https://picsum.photos/600/400?random=2' },
		{ id: 3, title: 'Project Three', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.', projectImage: 'https://picsum.photos/600/400?random=3' },
		{ id: 4, title: 'Project Four', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.', projectImage: 'https://picsum.photos/600/400?random=4' },
		{ id: 5, title: 'Project Five', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.', projectImage: 'https://picsum.photos/600/400?random=5' },
		{ id: 6, title: 'Project Six', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.', projectImage: 'https://picsum.photos/600/400?random=6' },
		{ id: 7, title: 'Project Seven', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.', projectImage: 'https://picsum.photos/600/400?random=7' },
		{ id: 8, title: 'Project Eight', description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed vitae sapien nec magna viverra scelerisque.', projectImage: 'https://picsum.photos/600/400?random=8' }
	];

	onMount(() => {
		// Heading animation
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
				start: 'top 80%'
			}
		});

		// Paragraph line-by-line
		const lines = splitIntoLines(paraEl);
		gsap.from(lines, {
			yPercent: 100,
			opacity: 0,
			duration: 0.8,
			stagger: 0.15,
			ease: 'power3.out',
			scrollTrigger: {
				trigger: paraEl,
				start: 'top 85%'
			}
		});

		// Projects scroll animation
		let tl2 = gsap.timeline({
			scrollTrigger: {
				trigger: '#projectGrid',
				scroller: 'body',
				start: 'top 50%',
				end: 'top 0',
				scrub: 2
			}
		});

		tl2.from(
			'#projectGrid .projcard.leftCard',
			{ x: -300, opacity: 0, duration: 0.5 },
			'proAniCard'
		);

		tl2.from(
			'#projectGrid .projcard.rightCard',
			{ x: 300, opacity: 0, duration: 0.5 },
			'proAniCard'
		);
	});

	onDestroy(() => {
		ScrollTrigger.getAll().forEach((t) => t.kill());
	});

	function splitIntoLines(element: HTMLElement) {
		const text = element.innerHTML;
		element.innerHTML = '';

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

			if (currentLine.offsetHeight > testSpan.offsetHeight * 1.5) {
				currentLine.removeChild(testSpan);
				currentLine = document.createElement('div');
				currentLine.className = 'overflow-hidden leading-relaxed';
				element.appendChild(currentLine);
				currentLine.appendChild(testSpan);
				lines.push(currentLine);
			}
		});

		lines.forEach((line) => {
			const inner = document.createElement('span');
			inner.className = 'block';
			inner.innerHTML = line.innerHTML;
			line.innerHTML = '';
			line.appendChild(inner);
		});

		return element.querySelectorAll('div > span');
	}

	// Card hover
	const cardHover = (selector: string) => {
		gsap.to(selector, { scale: 1.1 });
	};
	const cardHoverLeft = (selector: string) => {
		gsap.to(selector, { scale: 1 });
	};

	// Click animation
	function openProject(event: MouseEvent, project: typeof projects[0]) {
		event.preventDefault();
		const card = event.currentTarget as HTMLElement;
		const bgDiv = card.querySelector('.bgImage') as HTMLElement;
		const rect = bgDiv.getBoundingClientRect();

		const clone = bgDiv.cloneNode(true) as HTMLElement;
		clone.style.position = 'fixed';
		clone.style.left = `${rect.left}px`;
		clone.style.top = `${rect.top}px`;
		clone.style.width = `${rect.width}px`;
		clone.style.height = `${rect.height}px`;
		clone.style.zIndex = '9999';
		clone.style.backgroundSize = 'cover';
		document.body.appendChild(clone);

		gsap.to(clone, {
			left: 0,
			top: 0,
			width: window.innerWidth,
			height: window.innerHeight,
			duration: 0.8,
			ease: 'power3.inOut',
			onComplete: () => {
				goto(`/project/${project.id}`);
			}
		});
	}
</script>

<svelte:head>
	<title>Projects | HMS</title>
</svelte:head>

<section class="w-full">
	<div class="px-4">
		<section class="w-full pt-32">
			<h1 bind:this={headingEl} class="text-[256px] leading-none font-bold">Work</h1>
			<p bind:this={paraEl} class="mt-8 max-w-3xl text-lg leading-relaxed">
				Lorem ipsum dolor sit amet consectetur, adipisicing elit. Rerum suscipit officiis temporibus
				non explicabo in aliquid maiores ab nam quos architecto, voluptates nisi enim quod natus,
				asperiores culpa dolorem dignissimos. Perferendis, laborum, numquam ducimus repudiandae
				incidunt aliquid praesentium tempore autem quam consequuntur neque reiciendis iste?
			</p>
		</section>

		<!-- Projects Section -->
		<section class="mt-24 grid gap-y-16 gap-x-32 md:grid-cols-2" id="projectGrid">
			{#each projects as project, i}
				<a
					href={`/project/${project.id}`}
					class="group projcard relative block overflow-hidden rounded-xl shadow-lg"
					class:leftCard={i % 2 === 0}
					class:rightCard={i % 2 !== 0}
					id={`projcard_${i}`}
					onmouseenter={() => cardHover(`#projcard_${i}`)}
					onmouseleave={() => cardHoverLeft(`#projcard_${i}`)}
					onclick={(e) => openProject(e, project)}
				>
					<div
						class="bgImage h-[320px] bg-cover bg-center"
						style={`background-image: url('${project.projectImage}')`}
					></div>
					<div class="absolute inset-0 bg-black/40 transition-colors group-hover:bg-black/60"></div>
					<div class="absolute bottom-4 left-4 text-white">
						<h3 class="text-2xl font-semibold">{project.title}</h3>
						<p class="mt-1 max-w-xs text-sm">{project.description}</p>
					</div>
				</a>
			{/each}
		</section>
	</div>
</section>

<style>
	.inner {
		display: inline-block;
	}
</style>
