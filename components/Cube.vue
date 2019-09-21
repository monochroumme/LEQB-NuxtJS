<template>
	<div id="cube"></div>
</template>

<script>
	import * as THREE from 'three';

	export default {
		data() {
			return {
				camera: '',
				scene: '',
				renderer: '',
				mesh: ''
			};
		},

		mounted() {
			this.init();
			this.animate();
		},

		methods: {
			init() {
				let frustumSize = 1000,
					boxSize = 400,
					aspect = 1;

				this.camera = new THREE.OrthographicCamera(frustumSize * aspect / - 2, frustumSize * aspect / 2, frustumSize / 2, frustumSize / - 2, 1, 1000);
				this.camera.position.z = 500;
				this.scene = new THREE.Scene();

				const geometry = new THREE.BoxBufferGeometry(boxSize, boxSize, boxSize);
				let envMap = new THREE.CubeTextureLoader()
										.setPath('')
										.load(['clouds.jpg', 'clouds.jpg', 'clouds.jpg', 'clouds.jpg', 'clouds.jpg', 'clouds.jpg']);
				const material = new THREE.MeshBasicMaterial({envMap});
				material.envMap.mapping = THREE.CubeRefractionMapping;
				this.mesh = new THREE.Mesh(geometry, material);
				this.scene.add(this.mesh);

				this.renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
				this.renderer.setPixelRatio( window.devicePixelRatio );
				this.renderer.setSize( boxSize, boxSize );
				document.getElementById('cube').appendChild(this.renderer.domElement);
			},

			animate() {
				requestAnimationFrame(this.animate);
				this.mesh.rotation.x += 0.002;
				this.mesh.rotation.y += 0.002;
				this.renderer.render(this.scene, this.camera);
			}
		}
	};
</script>