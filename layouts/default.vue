<template>
  <div id="page">
    <Menu />
    <div id="page-content" :style="{ 'right': right, 'left': left }">
      <nuxt />
    </div>
  </div>
</template>

<script>
  import Menu from '~/components/Menu';
  
  export default {
    data() {
      return {
        right: 0,
        left: 0
      };
    },

    mounted() {
      let menuItems = document.getElementsByClassName('menu__item');
      let right = 0;

      for (let i = 0; i < menuItems.length; i++) {
        right += menuItems[i].offsetWidth;
      }

      this.right = right + "px";
    },

    components: {
      Menu
    }
  }
</script>

<style>
  @font-face {
    font-family: 'Biotif';
    src: url('~static/fonts/biotif/Biotif-Regular.ttf');
  }

  @font-face {
    font-family: 'Biotif-Light';
    src: url('~static/fonts/biotif/Biotif-Light.ttf');
  }

  @font-face {
    font-family: 'Biotif-LightItalic';
    src: url('~static/fonts/biotif/Biotif-LightItalic.ttf');
  }

  html {
    font-size: 16px;
    word-spacing: 1px;
    -ms-text-size-adjust: 100%;
    -webkit-text-size-adjust: 100%;
    -moz-osx-font-smoothing: grayscale;
    -webkit-font-smoothing: antialiased;
    box-sizing: border-box;
  }

  body {
    font-family: 'Biotif' !important;
    position: relative;
    background: #F7F7F7;
    height: 100vh;
    color: black;
  }

  *,
  *:before,
  *:after {
    box-sizing: border-box;
    margin: 0;
  }

  #page-content {
    position: absolute;
    transition: all 1s;
  }

  .content {
    margin: 0 110px;
    position: relative;
  }

  .italic {
    font-family: 'Biotif-LightItalic';
  }
</style>
