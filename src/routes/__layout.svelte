<div class="_container">
	<filter id="dropshadow" height="130%">
		<feGaussianBlur in="SourceAlpha" stdDeviation="3" />
		<!-- stdDeviation is how much to blur -->
		<feOffset dx="2" dy="2" result="offsetblur" />
		<!-- how much to offset -->
		<feComponentTransfer>
			<feFuncA type="linear" slope="0.7" />
			<!-- slope is the opacity of the shadow -->
		</feComponentTransfer>
		<feMerge>
			<feMergeNode />
			<!-- this contains the offset blurred image -->
			<feMergeNode in="SourceGraphic" />
			<!-- this contains the element that the filter is applied to -->
		</feMerge>
	</filter>
	<slot />
</div>

<style global>
	html,
	body,
	#svelte {
		height: 100%;
		background-color: black;
		margin: 0;
		overflow: hidden;
	}

	* {
		font-family: 'Nanum Barun Gothic';
	}

	h1 {
		color: white;
		margin-left: 16px;
	}

	._container {
		height: 100%;
	}

	.box {
		background-color: transparent;
		border: 1px solid white;
		box-shadow: 0px 0px 4px 2px white;
		color: white;
		text-align: center;
		border-radius: 16px;
		padding: 16px;
		font-weight: bold;
		font-size: 32px;
	}
</style>
