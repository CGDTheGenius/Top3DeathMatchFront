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
	$: winner = [-1, 0, 1].includes(status.last_winner)
		? status.last_winner === -1
			? null
			: status.players[status.last_winner].name
		: undefined;
	$: {
		if (winner !== undefined) appear = true;
	}
	let appear = false;

	const fetchStatus = async () => {
		const res = await fetch('http://dev.holenet.net:5000/status');
		status = await res.json();
	};

	fetchStatus();

	const handleMakeBet = async (index) => {
		let value = prompt('제시할 포인트를 입력해주세요.');
		try {
			value = parseInt(value);
			await fetch(`http://dev.holenet.net:5000/bet/${index}/`, {
				method: 'POST',
				body: value.toString()
			});
			fetchStatus();
		} catch (error) {
			alert('유효하지 않은 값입니다.');
		}
	};

	const handleMakeRound = async () => {
		if (confirm('라운드를 진행하시겠습니까?')) {
			const res = await fetch(`http://dev.holenet.net:5000/round/`, {
				method: 'POST'
			});
			const win = await res.json();
			fetchStatus();
		}
	};

	const addMorePoints = async (e) => {
		if (e.code === 'Space') {
			let value = prompt('몇 포인트를 추가하시겠습니까?');
			try {
				value = parseInt(value);
				await fetch('http://dev.holenet.net:5000/more/', {
					method: 'POST',
					body: value.toString()
				});
				fetchStatus();
			} catch (error) {
				alert('유효하지 않은 값입니다.');
			}
		}
	};

	setInterval(fetchStatus, 1000);
</script>

<svelte:window on:keydown={addMorePoints} />

<div class="container">
	<div class="score">
		<Score players={status.players} hidden={false} />
	</div>
	<div class="header">
		<div on:click={() => handleMakeBet(0)}>
			<Player
				player={status.players[0]}
				isFirst={status.first === 0}
				isTurn={nextTurn === 0}
				isWinner={status.last_winner === 0}
				hidden={false}
			/>
		</div>
		<div class="box round" on:click={handleMakeRound}>
			Round {status.round}
		</div>
		<div on:click={() => handleMakeBet(1)}>
			<Player
				player={status.players[1]}
				isFirst={status.first === 1}
				isTurn={nextTurn === 1}
				isWinner={status.last_winner === 1}
				right={true}
				hidden={false}
			/>
		</div>
	</div>
	<div class="body">
		<Point point={status.players[0].point} hidden={false} />
		<!-- <Scale bettings={status.players.map((p) => p.betting)} /> -->
		<Betting bettings={status.players.map((p) => p.betting)} />
		<Point point={status.players[1].point} hidden={false} />
	</div>
	<!-- <Winner {winner} {appear} /> -->
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
