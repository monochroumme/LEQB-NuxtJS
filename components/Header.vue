<template>
	<div class="header">
		<transition name="fade">
			<a href="/" v-show="showLogo">
				<img alt="Logo" src="~/static/logo.png" >
			</a>
		</transition>
		<transition name="fade">
			<a id="drop" href="#" class="line" v-show="showDrop">
				Drop request
			</a>
		</transition>
	</div>
</template>

<script>
	export default {
		props: [
			'color', // no use for now
			'showLogo',
			'showDrop'
		]
	};
</script>

<style scoped>
	.header {
		display: flex;
		justify-content: space-between;
		align-items: center;
		width: 100%;
		letter-spacing: 1px;
		text-transform: uppercase;
		color: black;
		position: absolute;
		top: 0;
	}

	img {
		width: 49px;
		height: 49px;
	}

	#drop {
		display: block;
		color: black;
		text-decoration: none;
	}

	.fade-enter-active, .fade-leave-active {
    	transition: opacity .5s;
	}

	.fade-enter, .fade-leave-to {
	    opacity: 0;
	}

	.line {
		position: relative;
	}

	.line:after {
		content: '';
		height: 3px;
		position: absolute;
		bottom: 0;
		width: 100%;
		background: black;
		transition: 0.3s;
		left: 0;
		right: auto;
	}

	.line:hover:after {
		right: 0;
		left: auto;
		width: 0%;
	}
</style>