<script>
	import Arm from './Arm.svelte';
	import { spring } from 'svelte/motion';

	export let bettings;

	$: bet0 = bettings[0];
	$: bet1 = bettings[1];

	let rotationValue = 0;
	const rotation = spring(0, {
		stiffness: 0.1,
		damping: 0.25
	});

	setInterval(() => {
		// const v = Math.round(Math.random() * 10 - 5);
		rotationValue = rotationValue === 5 ? -5 : 5;
		rotation.set(rotationValue);
	}, 300);
</script>

<div class="container">
	<div class="scale" />
	<div class="scale-bottom" />
	<Arm rotation={$rotation} />
</div>

<style>
	.container {
		width: 100%;
		height: calc(100% - 16px);
		/* background-color: salmon; */
		margin: 16px;
	}

	.scale {
		position: absolute;
		left: calc(50% - 20px);
		width: 40px;
		height: 500px;
		bottom: 16px;
		background-color: white;
		border-radius: 20px;
	}

	.scale-bottom {
		position: absolute;
		left: calc(50% - 100px);
		height: 40px;
		width: 200px;
		bottom: 16px;
		background-color: white;
		border-top-right-radius: 40px;
		border-top-left-radius: 40px;
	}
</style>
