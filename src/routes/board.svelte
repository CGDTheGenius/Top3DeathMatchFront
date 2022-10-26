<script>
	import Player from '../lib/Player.svelte';
	import Point from '../lib/Point.svelte';
	import Betting from '../lib/Betting.svelte';
	import Score from '../lib/Score.svelte';

	let status = {
		players: [
			{
				point: 100,
				bettings: []
			},
			{
				point: 100,
				bettings: []
			}
		],
		first: 0
	};
	$: nextTurn =
		status.players[status.first].betting === null
			? status.first
			: status.players[1 - status.first].betting === null
			? 1 - status.first
			: -1;

	const fetchStatus = async () => {
		const res = await fetch('http://dev.holenet.net:5000/status');
		status = await res.json();
	};

	fetchStatus();

	const handleNext = async (e) => {
		if (e.code === 'Enter') fetchStatus();
	};

	setInterval(fetchStatus, 1000);
</script>

<svelte:window on:keydown={handleNext} />

<div class="container">
	<div class="score">
		<Score players={status.players} />
	</div>
	<div class="header">
		<div>
			<Player
				player={status.players[0]}
				isFirst={status.first === 0}
				isTurn={nextTurn === 0}
				isWinner={status.last_winner === 0}
			/>
		</div>
		<div class="box round">
			Round {status.round}
		</div>
		<div>
			<Player
				player={status.players[1]}
				isFirst={status.first === 1}
				isTurn={nextTurn === 1}
				isWinner={status.last_winner === 1}
				right={true}
			/>
		</div>
	</div>
	<div class="body">
		<Point point={status.players[0].point} />
		<!-- <Scale bettings={status.players.map((p) => p.betting)} /> -->
		<Betting bettings={status.players.map((p) => p.betting)} />
		<Point point={status.players[1].point} />
	</div>
</div>

<style>
	.container {
		display: flex;
		flex-direction: column;
		height: 100%;
	}

	.score {
		margin-top: 20px;
	}

	.header {
		width: 100%;
		margin-top: 20px;
		display: flex;
		justify-content: space-around;
		align-items: center;
	}

	.body {
		width: 100%;
		margin-top: 20px;
		margin-bottom: 20px;
		display: flex;
		justify-content: space-around;
		flex: 1 1 0;
	}

	.round {
		height: fit-content;
	}
</style>
