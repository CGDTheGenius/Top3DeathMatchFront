<script>
	export let players;
	export let hidden = true;

	$: length = Math.max(9, players[0].bettings.length);
	let winners;
	$: {
		winners = [];
		for (let i = 0; i < players[0].bettings.length; ++i) {
			winners.push(
				players[0].bettings[i] > players[1].bettings[i]
					? 0
					: players[0].bettings[i] < players[1].bettings[i]
					? 1
					: -1
			);
		}
	}
</script>

<div class="box container">
	<table class="table">
		<tr style="border-bottom: 1px solid white">
			<th style="border-right: 1px solid white">R</th>
			{#each { length } as _, round}
				<th>
					{round + 1}
				</th>
			{/each}
		</tr>
		<tr>
			<th style="border-right: 1px solid white">{players[0].name}</th>
			{#each players[0].bettings as betting, i}
				<td class:winner={winners[i] === 0}
					>{@html hidden ? (winners[i] === 0 ? '●' : '&nbsp;&nbsp;') : betting}</td
				>
			{/each}
		</tr>
		<tr>
			<th style="border-right: 1px solid white">{players[1].name}</th>
			{#each players[1].bettings as betting, i}
				<td class:winner={winners[i] === 1}
					>{@html hidden ? (winners[i] === 1 ? '●' : '&nbsp;&nbsp;') : betting}</td
				>
			{/each}
		</tr>
	</table>
</div>

<style>
	.container {
		width: calc(100% - 72px);
		margin: 16px;
		display: flex;
		justify-content: space-between;
	}

	.table {
		width: 100%;
		text-align: center;
		border-collapse: collapse;
	}

	.winner {
		color: red;
		text-shadow: 0px 0px 10px red;
	}
</style>
