<template>
	<svg id="main-line-svg">
		<path id="main-line-hitbox" fill="none" stroke="transparent" stroke-width="40" @mouseover="shake()" />
		<path id="main-line-path" fill="none" stroke="black" stroke-width="2" />
	</svg>
</template>

<script>
	export default {
		data() {
			return {
				diagonal: {
					elasticness: 0.01,
					elasticDuration: 1000,
					touchedTime: 0,
					touched: false
				}
			};
		},

		mounted() {
			this.render();
		},

		methods: {
			render() {
				window.requestAnimationFrame(this.render);
				this.update();
			},

			update() {
				let line = document.getElementById('main-line-path');
				let hitbox = document.getElementById('main-line-hitbox');
				let svg = document.getElementById('main-line');
				let startX = (svg.offsetWidth - svg.offsetHeight) / 2,
					startY = svg.offsetHeight,
					endX = (svg.offsetWidth + svg.offsetHeight) / 2,
					endY = 0,
					midX = svg.offsetWidth / 2,
					midY = svg.offsetHeight / 2,
					elastok = 1;

				if (this.diagonal.touched) {
					let t = (Date.now() - this.diagonal.touchedTime) / this.diagonal.elasticDuration,
						p = this.diagonal.elasticness;

					if (t < (this.diagonal.elasticDuration / 1000)) {
						elastok = (Math.pow(2,-10*t) * Math.sin((t-p/4)*(2*Math.PI)/p) + 1);
					} else {
						this.diagonal.touched = false;
						elastok = 1;
					}
				}

				if (svg.offsetHeight && svg.offsetWidth) {
					line.setAttribute('d', `M ${startX} ${startY} Q ${midX} ${midY*elastok} ${endX} ${endY}`);
					hitbox.setAttribute('d', `M ${startX} ${startY} Q ${midX} ${midY} ${endX} ${endY}`);
				}
			},

			shake() {
				this.diagonal.touchedTime = Date.now();
				this.diagonal.touched = true;
			}
		}
	};
</script>

<style scoped>
#main-line-svg {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    overflow: visible;
}
</style>