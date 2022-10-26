<script>
	export let player;
	export let isFirst;
	export let isTurn;
	export let right = false;
	export let isWinner = false;
	export let hidden = true;

	$: isDone = player.betting !== null;
</script>

<div class="container" class:winner={isWinner}>
	{#if player}
		<div
			class="box header"
			class:active={isTurn}
			class:done={isDone}
			style="flex-direction: {right ? 'row-reverse' : 'row'}"
		>
			<div class="wins">
				{player.wins}승
			</div>
			<div class="name">
				{player.name}
			</div>
			<!-- <div class="first">
				{isFirst ? '선공' : '후공'}
			</div> -->
		</div>
		{#if !hidden}
			<div
				class="box bettings"
				class:invisible={player.betting === undefined || player.betting === null}
			>
				<div class="betting">
					{@html player.betting === undefined || player.betting === null
						? '&nbsp;'
						: player.betting}
				</div>
			</div>
		{/if}
	{/if}
</div>

<style>
	.container {
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.header {
		display: flex;
		gap: 16px;
		margin: 16px;
	}

	.active {
		position: relative;
		box-shadow: 0px 0px 14px 7px salmon, 0px 0px 1px 1px red;
		z-index: 1;
		animation: 1s cubic-bezier(0, 1.48, 0.27, 0.88) highlight-active;
	}

	.done {
		position: relative;
		box-shadow: 0px 0px 14px 7px aquamarine, 0px 0px 1px 1px aquamarine;
		z-index: 1;
	}

	.winner {
		animation: 2s cubic-bezier(0, 1.48, 0.27, 0.88) highlight-winner;
	}

	.bettings {
		display: flex;
		gap: 8px;
		padding: 8px;
	}

	.bettings.invisible {
		border: none;
		box-shadow: none;
	}

	.betting {
		font-size: 16px;
		color: white;
	}

	@keyframes highlight-winner {
		100% {
			transform: rotateZ(720deg) scale(1);
			opacity: 1;
		}
		0% {
			transform: rotateZ(0deg) scale(0);
			opacity: 0;
		}
	}

	@keyframes highlight-active {
		100% {
			transform: rotateZ(0deg) scale(1);
		}
		0% {
			transform: rotateZ(0deg) scale(0.5);
			opacity: 0.5;
		}
	}
</style>
