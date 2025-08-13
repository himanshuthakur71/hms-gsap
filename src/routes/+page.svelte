<script lang="ts">
	import FeedBack from '$lib/components/Feedback.svelte';
	import Hero from '$lib/components/Hero.svelte';
	import HorizontalScroll from '$lib/components/HorizontalScroll.svelte';
	import Info from '$lib/components/Info.svelte';
	import Prallex from '$lib/components/Prallex.svelte';
	import Process from '$lib/components/Process.svelte';
</script>

<HorizontalScroll>
	<Hero />
	<Info />
</HorizontalScroll>

<!-- Normal scroll section -->
<Prallex />
<Process />
<FeedBack />