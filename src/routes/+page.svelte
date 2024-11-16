<script lang="ts">
	import { onMount } from 'svelte';
	import gsap from 'gsap';
	import ScrollTrigger from 'gsap/ScrollTrigger';
	import SplitType from 'split-type';

	onMount(() => {
		gsap.registerPlugin(ScrollTrigger);

		const texts = document.querySelectorAll('.animate-text') as NodeListOf<HTMLElement>;
		texts.forEach((text) => {
			new SplitType(text, { types: 'words' });

			text.querySelectorAll('.word').forEach((word) => {
				const wrapper = document.createElement('div');
				wrapper.style.overflow = 'hidden';
				wrapper.style.display = 'inline-block';
				if (word.parentNode) {
					word.parentNode.insertBefore(wrapper, word);
					wrapper.appendChild(word);
				}
			});

			// Animate each word
			gsap.from(text.querySelectorAll('.word'), {
				scrollTrigger: {
					trigger: text,
					start: 'top 80%',
					toggleActions: 'play none none none'
				},
				duration: 0.8,
				y: 100,
				opacity: 0,
				stagger: 0.02,
				ease: 'power3.out'
			});
		});
	});
</script>

<div class="p-8">
	<h1 class="animate-text text-3xl font-semibold">Welcome to Kriyavat Labs</h1>
	<p class="animate-text mt-10 text-4xl font-semibold leading-relaxed text-neutral-400">
		We are just team of tech bros who are tired of “building the next thing” and “disrupting the
		industry” yapping. Just pure - unadulterated love for building stuff and code. We build and ship
		projects, because, well, that's what we love. No startup ambitions. Just solid side projects.
	</p>
	<p class="animate-text mt-10 text-4xl font-semibold leading-relaxed text-neutral-400">
		Why? We are just starting out now, cooking up our first project. So why Kriyavat Labs?
		<br /> Simple - we want a place to showcase our projects and space where we build things we find
		interesting and share them with others who might find them useful.
		<br />
		And maybe, just maybe, create something that makes someone out there go “Huh, that's pretty sick.”
		No big promises. Just projects fuelled by caffeine, curiosity, and some Rock music. And our favourite
		phrase is “just another side project”
	</p>
</div>

<style>
	/* p {
		mix-blend-mode: multiply;
	} */
</style>
