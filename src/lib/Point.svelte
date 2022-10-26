<script>
	export let point;
	export let hidden = true;
</script>

<div class="container">
	<div class="interval" class:active={80 <= point} style="background-color: #ffdddd">
		<div class="point" class:hidden>{point}</div>
	</div>
	<div class="interval" class:active={60 <= point && point < 80} style="background-color: #ff9999">
		<div class="point" class:hidden>{point}</div>
	</div>
	<div class="interval" class:active={40 <= point && point < 60} style="background-color: #ff6666">
		<div class="point" class:hidden>{point}</div>
	</div>
	<div class="interval" class:active={20 <= point && point < 40} style="background-color: #ff3333">
		<div class="point" class:hidden>{point}</div>
	</div>
	<div class="interval" class:active={0 <= point && point < 20} style="background-color: #ff0000">
		<div class="point" class:hidden>{point}</div>
	</div>
</div>

<style>
	.container {
		margin: 16px;
		height: calc(100% - 32px);
		width: 64px;
	}

	.interval {
		justify-self: flex-end;
		height: 20%;
		display: flex;
		justify-content: center;
		align-items: center;
		opacity: 0.5;
	}

	.active {
		position: relative;
		box-shadow: 0px 0px 14px 7px red, 0px 0px 1px 1px red;
		opacity: 1;
		z-index: 1;
	}

	.point {
		display: none;
	}
	.active .point {
		display: block;
		font-size: 24px;
		font-weight: bold;
	}

	.point.hidden {
		display: none;
	}
</style>
