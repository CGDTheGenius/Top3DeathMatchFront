<script>
	import { spring } from 'svelte/motion';
	import { fade } from 'svelte/transition';

	export let bettings;

	$: bet0 = bettings[0];
	$: bet1 = bettings[1];
	$: both = bettings[0] !== null && bettings[1] !== null;

	let ratioValue = 0.0;
	const ratio = spring(0, {
		stiffness: 0.1,
		damping: 0.25
	});

	setInterval(() => {
		ratioValue = ratioValue === 0.0 ? 1.0 : 0.0;
		ratio.set(ratioValue);
	}, 200);
</script>

<div class="container">
	{#each bettings as betting, index}
		<div class="wrapper">
			{#if betting !== undefined && betting !== null}
				<div
					class="text"
					transition:fade
					style="font-size: {both ? (index === 0 ? $ratio : 1 - $ratio) * 100 + 100 : 150}px;"
				>
					?
				</div>
				{#if betting >= 10}
					<div
						transition:fade
						class="hint"
						style="font-size: {both ? (index === 0 ? $ratio : 1 - $ratio) * 10 + 30 : 30}px;"
					>
						10+
					</div>
				{/if}
			{/if}
		</div>
	{/each}
</div>

<style>
	.container {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		/* gap: 50px; */
	}

	.wrapper {
		margin-top: auto;
		height: 400px;
		color: white;
		width: 400px;
		display: flex;
		justify-content: flex-end;
		align-items: center;
		margin-bottom: 100px;
		font-weight: bold;
		flex-direction: column;
	}
</style>
