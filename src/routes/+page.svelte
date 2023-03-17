<script>
	import { onMount } from 'svelte';
	import lottie from 'lottie-web';
	import fireworks from '$lib/fireworks.json';

	let lottieElement;
	let startAnimation;
	onMount(async () => {
		startAnimation = lottie.loadAnimation({
			container: lottieElement,
			renderer: 'svg',
			animationData: fireworks,
			loop: false,
			autoplay: false
		});
		startAnimation.goToAndStop(150, true);
		// const lastFrame = startAnimation.totalFrames - 1;
		// startAnimation.goToAndStop(lastFrame, true);
	});
	async function buttonClicked() {
		// startAnimation.goToAndStop(150, true);
		console.log('Button clicked');
		// startAnimation.goToAndPlay(1, true);

		// Create a Promise that resolves when the animation completes
		const animationPromise = new Promise((resolve) => {
			startAnimation.playSegments([[1, 75]], true);
			startAnimation.addEventListener('complete', resolve);
		});

		// Wait for the Promise to resolve before logging the next step
		await animationPromise;

		console.log('Next step');
		startAnimation.goToAndStop(150, true);
		// startAnimation.destroy();
	}
</script>

<main>
	<h1 class=".lottie-element text-3xl font-bold">This is lottie animation tutorial process</h1>
	<div class="w-1/2 h-96 ring " bind:this={lottieElement}>Hello world</div>
	<button on:click={buttonClicked} class="btn btn-primary btn-xl w-1/2"> Buy Now </button>
</main>
