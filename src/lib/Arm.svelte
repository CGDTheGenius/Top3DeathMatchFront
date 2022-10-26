<script>
	export let rotation;
</script>

<div class="container" style="transform: rotate({rotation}deg);">
	<div class="scale" />
	<div class="scale-left" />
	<div class="scale-right" />
</div>

<style>
	.container {
		position: relative;
		height: calc(100% - 16px);
		transform-origin: 50% calc(50% - 80px);
	}

	.scale {
		position: absolute;
		left: calc(50% - 250px);
		top: calc(50% - 10px);
		height: 20px;
		width: 500px;
		background-color: white;
		border-radius: 10px;
	}

	.scale-left {
		position: absolute;
		left: calc(50% - 250px);
		top: calc(50% - 48px);
		height: 10px;
		width: 250px;
		background-color: white;
		border-radius: 10px;
		transform: rotate(-18deg);
	}
	.scale-right {
		position: absolute;
		right: calc(50% - 250px);
		top: calc(50% - 48px);
		height: 10px;
		width: 250px;
		background-color: white;
		border-radius: 10px;
		transform: rotate(18deg);
	}
</style>
