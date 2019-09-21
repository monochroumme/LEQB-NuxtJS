<template>
	<div id="menu">
		<a v-for="(link, index) in links" 
			:key="index" :href="link.href" 
			:class="leftOrRight(index) ? 'menu__item-border-left' : 'menu__item-border-right'" 
			:style="{'display': link.display, 'right': link.right, 'left': link.left}"
			class="menu__item">
			<div class="menu__item-title">{{ link.title }}</div>
		</a>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				links: [
					{
						href: '/',
						display: 'none',
						title: 'Main',
						right: 0,
						left: 'auto'
					},
					{
						href: '#',
						display: '',
						title: 'Projects',
						right: 0,
						left: 'auto'
					},
					{
						href: '#',
						display: '',
						title: 'About Us',
						right: 0,
						left: 'auto'
					},
					{
						href: '#',
						display: '',
						title: 'Contacts',
						right: 0,
						left: 'auto'
					}
				]
			};
		},

		mounted() {
			let menuItems = document.getElementsByClassName('menu__item');
			let offset = menuItems.length-1; // -1 because one is hidden

			for (let i = 0; i < menuItems.length; i++) {
				this.links[i].right = offset * menuItems[i].offsetWidth + 'px';
				offset -= 1;
				menuItems[i].style.animationDuration = 1 + i/10 + 's';
			}
		},

		methods: {
			leftOrRight(index) {
				if (this.links[index].right == 'auto')
					return false;
				else if (this.links[index].left == 'auto')
					return true;
			}
		}
	}
</script>

<style scoped>
	#menu {
		position: absolute;
		width: 100%;
		height: 100%;
	}

	.menu__item {
		position: absolute;
		bottom: 0;
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		text-decoration: none;
		text-transform: uppercase;
		animation-name: menuAnimation;
		animation-timing-function: ease;
		animation-duration: 1.5s;
		animation-delay: 1.6s;
		animation-fill-mode: forwards;
		text-align: center;
		transform: translateY(-100%);
		width: 35px;
		transition: left 1s, right 1s;
	}

	.menu__item:hover {
		background-image: url('~static/menuBg.gif');
		background-size: cover;
		background-repeat: no-repeat;
	}

	.menu__item-title {
		color: black;
		font-weight: bolder;
  		transform: rotate(-90deg);
  		font-size: 12px;
		line-height: 100%;
  		letter-spacing: 1px;
  		white-space: nowrap;
  		background-blend-mode: difference;
  		    font-weight: bolder;
    transform: rotate(-90deg);
    font-size: 12px;
    line-height: 100%;
    /* width: 40px; */
    letter-spacing: 1px;

	}

	.menu__item:hover .menu__item-title {
		color: red;
	    background: url('~static/menuBg.gif') !important;
	    background-clip: text !important;
	    -webkit-background-clip: text !important;
	    -webkit-text-fill-color: transparent !important;
	}

	.menu__item-border-left {
		border-left: 1px solid rgba(0, 0, 0, 0.1);
	}

	.menu__item-border-right {
		border-right: 1px solid rgba(0, 0, 0, 0.1);
	}

	@keyframes menuAnimation {
	  0% {
	    transform: translateY(-100%);
	    opacity: 0;
	    clip-path: polygon(100% 0, 100% 100%, 0 100%, 0 80%);
	  }
	  100% {
	    transform: translateY(0);
	  }
	}
</style>