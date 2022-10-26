<script>
	export let winner;
	$: winner, (appear = true);
	let appear = false;
	let none = false;

	const handleEnd = () => {
		none = !appear;
		setTimeout(() => (appear = false), 5000);
	};
</script>

<div class="container">
	<div class="banner" class:appear class:disappear={!appear} on:animationend={handleEnd} class:none>
		{#if winner !== undefined}
			{winner === null ? '무승부' : `${winner} 승`}
		{/if}
	</div>
</div>

<style>
	.container {
		position: absolute;
		width: 100%;
		height: 100%;
		z-index: 100;
		pointer-events: none;
		display: flex;
		justify-content: center;
		align-items: center;
	}

	.banner {
		color: white;
		transform-origin: 50% 50% 500px;
		font-size: 100px;
		font-weight: bold;
	}

	.appear {
		animation: 1s cubic-bezier(0, 1.48, 0.88, 0.86) spin;
	}

	.disappear {
		animation: 1s cubic-bezier(0.14, 0.15, 1, -0.36) spin2;
	}

	.none {
		display: none;
	}

	@keyframes spin {
		100% {
			transform: rotateX(0deg) rotateY(0deg);
		}
		0% {
			transform: rotateX(0deg) rotateY(180deg) scale(0);
			opacity: 0;
		}
	}

	@keyframes spin2 {
		0% {
		}
		100% {
			transform: scale(0);
			opacity: 0;
		}
	}
</style>
