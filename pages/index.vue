<template>
  <div id="main" class="content">
    <div id="main-content">
      <transition name="fade">
        <div id="main-line" v-show="showLineAndMenus">
          <MainLine />
        </div>
      </transition>
      <Header color="black" :showLogo="showLogo" :showDrop="showDrop" />
      <transition name="fade">
        <div id="main-h1" v-show="showHeaders">
          <template v-for="(text, index) in header1">
            <span v-html="text"></span>
          </template>
        </div>
      </transition>
      <transition name="fade">
        <div id="main-cube" v-show="showCube">
          <Cube />
        </div>
      </transition>
      <transition name="fade">
        <div id="main-h2" v-show="showHeaders">
          <template v-for="(text, index) in header2">
            <span v-html="text"></span>
          </template>
        </div>
      </transition>
    </div>
    <div id="main-footer">
      <transition name="fade">
        <div class="main-footer__left" v-show="showFooter1">
          <a href="https://instagram.com/nexusgeniuz">Instagram</a>
          <a href="#">Behance</a>
        </div>
      </transition>
      <transition name="fade">
        <div class="main-footer__right" v-show="showFooter2">
          <span>info@le-qb.com</span>
          <span>+38.063.533.22.87</span>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
  import Header from '~/components/Header';
  import MainLine from '~/components/MainLine';
  import Cube from '~/components/Cube';

  export default {
    data() {
      return {
        showLogo: false,
        showDrop: false,
        showLineAndMenus: false,
        showHeaders: false,
        showFooter1: false,
        showFooter2: false,
        showCube: false,
        header1: ['Creative spaces', 'for life and business'],
        header2: ['The basic', 'philosophy of our', 'studio is to create', 'individual solutions.']
      };
    },

    components: {
      Header,
      MainLine,
      Cube
    },

    mounted() {
      this.italizeIO();

      this.showHeader(0.5, 2.1);
      this.showMainLine(1);
      this.showMainHeaders(1);
      this.showMainFooter1(2);
      this.showMainFooter2(2.2);
      this.showMainCube(2.3);
    },

    methods: {
      showHeader(showLogoTime, showDropTime) {
        // show logo
        setTimeout(() => {
          this.showLogo = true;
        }, showLogoTime * 1000);
        // show drop
        setTimeout(() => {
          this.showDrop = true;
        }, showDropTime * 1000);
      },

      showMainLine(showLineTime) {
        // show line
        setTimeout(() => {
          this.showLineAndMenus = true;
        }, showLineTime * 1000);
        // TODO show menus
      },

      showMainHeaders(showHeadersTime) {
        setTimeout(() => {
          this.showHeaders = true;
        }, showHeadersTime * 1000);
      },

      showMainFooter1(showTime) {
        setTimeout(() => {
          this.showFooter1 = true;
        }, showTime * 1000);
      },

      showMainFooter2(showTime) {
        setTimeout(() => {
          this.showFooter2 = true;
        }, showTime * 1000);
      },
      showMainCube(showTime) {
        setTimeout(() => {
          this.showCube = true;
        }, showTime * 1000);
      },

      italizeIO() {
        let header = this.header1.join('-')+'_'+this.header2.join('-');
        let indexes = [];
        header = header.replace(/i/g,`<span class="italic">i</span>`)
                       .replace(/o/g,`<span class="italic">o</span>`);

        let headers = header.split('_');
        this.header1 = headers[0].split('-');
        this.header2 = headers[1].split('-');

        // TODO flicker random I or O letters between regular and italic
      }
    }
  };
</script>

<style>
#main-line {
  height: 100%;
}

#main-content {
  flex-grow: 1;
  position: relative;
}

#main-cube {
  position: absolute;
  transform: translate(0, -50%);
  top: 50%;
  width: 50%;
  z-index: -1;
}

#main-h1, #main-h2 {
  display: flex;
  flex-direction: column;
  font-family: 'Biotif-Light';
}

#main-h1 {
  position: absolute;
  top: 0;
  margin-top: 7%;
  font-size: 26px;
  line-height: 140%;
  z-index: -1;
}

#main-h2 {
  position: absolute;
  bottom: 0;
  right: 0;
  text-transform: uppercase;
  font-size: 56px;
  line-height: 105%;
  text-align: right;
  z-index: -1;
}

#main-footer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 5%;
}

#main-footer a {
  color: black;
  text-decoration: none;
}

#main-footer a, #main-footer span {
  margin: 0 24px;
  text-transform: uppercase;
}

#main-footer a:first-child, #main-footer span:first-child {
  margin-left: 0;
}

#main-footer a:last-child, #main-footer span:last-child {
  margin-right: 0;
}

#main {
  padding: 50px 0;
  display: flex;
  flex-direction: column;
  height: 100vh;
  margin: 0 3%;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

#main-h1 > span, #main-h2 > span {
  width: 100%;
  float: left;
  clip-path: polygon(100% 0, 100% 100%, 0 100%, 0 80%);
  transform: translateY(-50px);
  opacity: 0;
  animation-name: titleAnimation;
  animation-timing-function: ease;
  animation-duration: 1s;
  animation-delay: 0.6s;
  animation-fill-mode: forwards;
}

#main-h1:first-child > span, #main-h2 > span:first-child {
  animation-delay: 0.7s;
}

#main-h1:last-child > span, #main-h2 > span:last-child {
  animation-delay: 0.5s;
}

@keyframes titleAnimation {
  0% {
    transform: translateY(-50px);
    opacity: 0;
    clip-path: polygon(100% 0, 100% 100%, 0 100%, 0 80%);
  }
  100% {
    transform: translateY(0);
    opacity: 1;
    clip-path: polygon(100% 0, 100% 100%, 0 100%, 0 0);
  }
}

@media (max-width: 1150px) {
  body {
    height: auto;
  }

  #main {
    height: initial;
    padding: 25px 0;
  }

  #page-content {
    right: 0 !important;
  }

  #main-h1, #main-h2 {
    position: initial;
  }

  #main-h1 {
    font-size: 18px;
    margin-top: 60px;
  }

  #main-h2 {
    font-size: 40px;
  }

  #drop {
    font-size: 14px;
  }

  #main-footer {
    font-size: 13px;
  }

  #main-cube {
    margin: 0;
    position: initial;
    transform: none;
    width: 100%;
  }

  #main-line {
    display: none;
  }
}

@media (max-width: 550px) {
  #main-h2 {
    font-size: 30px;
  }

  #main-footer {
    flex-direction: column;
    justify-content: center;
  }

  .main-footer__left, .main-footer__right {
    width: 100%;
    display: flex;
  }

  #main-footer a:first-child, #main-footer span:first-child {
    text-align: right;
  }

  #main-footer a, #main-footer span {
    width: 50%;
  }
}

@media (max-width: 350px) {
  #main-h2 {
    font-size: 25px;
  }

  #main-footer {
    font-size: 11px;
  }
}
</style>