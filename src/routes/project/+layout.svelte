<script lang="ts">
	import { afterNavigate, beforeNavigate } from '$app/navigation';
	import gsap from 'gsap';
	import { Flip } from 'gsap/Flip';

	gsap.registerPlugin(Flip);

	let { children } = $props();


    let st : Flip.FlipState

     beforeNavigate(() => {
        st = Flip.getState(".projectImage")
     })

     afterNavigate(() => {
        Flip.from(st, {
            targets: '.projectImage', 
            duration: 0.4,
            scale: true,
            ease:  'ease-out'
        })
     })
</script>

{@render children?.()}
