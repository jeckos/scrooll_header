<template>
  <div id="app">
    <header ref="header">
      <nav ref="nav">
        <h2 class="title">Dashboard</h2>
        <button>btn</button>
      </nav>
      <div class="btc" ref="btc">
        <div class="text" ref="text">
          <h3 ref="textTitle">0,00000 btc</h3>
          <span class="icon" ref="icon">icon</span>
        </div>
        <div class="bg" ref="bg"></div>
        <img alt=""
             ref="img"
             src="https://images.unsplash.com/flagged/photo-1564049380284-0d153ea79204?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1050&q=80">
      </div>
    </header>
    <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Ipsum laborum minus qui. Blanditiis consequatur
      corporis debitis ducimus eos ex, explicabo fugit harum ipsa ipsum laboriosam magnam maxime minus non optio,
      placeat qui quibusdam quo, repellendus similique sint unde vel voluptatibus. Accusamus animi aperiam at atque
      distinctio facilis fugiat hic ipsum minus modi non omnis pariatur quam quas quidem quo sit vel, voluptas
      voluptates voluptatum? Adipisci deserunt dignissimos dolorem earum eos nisi placeat quaerat, quis recusandae
      repellendus suscipit, tempore temporibus vero voluptates voluptatum. Aspernatur debitis et ex iste maiores maxime
      minima natus necessitatibus nobis quae quo quod repellat, suscipit tempora unde.</p>
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      elements: {
        header: null,
        nav: null,
        btc: null,
        bg: null,
        img: null,
        text: null,
        icon: null,
        textTitle: null
      }
    }
  },
  mounted () {
    this.header = this.$refs.header
    this.nav = this.$refs.nav
    this.btc = this.$refs.btc
    this.bg = this.$refs.bg
    this.img = this.$refs.img
    this.text = this.$refs.text
    this.textTitle = this.$refs.textTitle
    this.icon = this.$refs.icon

    //  getElmHeight(node) {
    //  const list = [
    //    'margin-top',
    //    'margin-bottom',
    //    'border-top',
    //    'border-bottom',
    //    'padding-top',
    //    'padding-bottom',
    //    'height'
    //  ]
    //
    //  const style = window.getComputedStyle(node)
    //  return list
    //    .map(k => parseInt(style.getPropertyValue(k)), 10)
    //    .reduce((prev, cur) => prev + cur)
    //
    // }

    window.addEventListener('scroll', (event) => {
      const wrapper = event.target
      const list = wrapper.firstElementChild || wrapper.firstChild
      let scrollTop = list.scrollTop

      let percentScrollNav = scrollTop * 100 / this.nav.offsetHeight
      if (percentScrollNav > 100) {
        this.header.style.backgroundColor = `rgba(255, 255, 255, 1)`
        this.bg.style.opacity = `.8`
        this.img.style.opacity = `.5`
      } else {
        this.header.style.backgroundColor = `rgba(255,255,255, ${percentScrollNav / 100})`
        this.bg.style.opacity = `${(percentScrollNav / 100 * 0.8)} `
        this.img.style.opacity = `${(percentScrollNav / 100 * 0.5)} `
        if (percentScrollNav <= 0) {
          this.img.style.opacity = ``
        }
      }
      this.nav.querySelector('.title').style.transform = `scale(${Math.max(0.4375, 1 - 0.005 * percentScrollNav)})`
      if (scrollTop > this.nav.offsetHeight) {
        this.btc.style.marginTop = `${this.nav.offsetHeight * -1}px`
        this.text.style.transform = `translateY(${this.nav.offsetHeight}px)`
      } else {
        this.btc.style.marginTop = `${scrollTop * -1}px`
        this.text.style.transform = `translateY(${scrollTop}px)`
      }
      if (percentScrollNav > 100) {
        this.textTitle.style.opacity = `0`
        this.icon.style.opacity = `1`
        this.textTitle.style.transform = `scale(0)`
        this.icon.style.transform = `scale(1)`
      } else {
        this.textTitle.style.opacity = `${1 - percentScrollNav / 100}`
        this.icon.style.opacity = `${percentScrollNav / 100}`
        this.textTitle.style.transform = `scale(${1 - percentScrollNav / 100})`
        this.icon.style.transform = `scale(${percentScrollNav / 100})`
      }
    })
  }

}
</script>

<style lang="scss">
  *, *:before, *:after {
    box-sizing: border-box;
  }

  body {
    background: #f5f5f5;
    margin: 0;
    padding: 0;
  }

  #app {
    max-width: 320px;
    margin: 0 auto;
    height: 120vh;
    padding-top: 336px;

    header {
      background-color: transparent;
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      transition: 0.1s;

      nav {
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-size: 34px;
        padding: 10px 10px;
        transition: .3s;
        position: relative;
        z-index: 2;
      }

      .text {
        position: absolute;
        z-index: 2;
        margin: 10px;

        h3 {
          margin: 0;

          font-size: 18px;
          transform-origin: left center;
        }

        .icon {
          position: absolute;
          top: 0;
          left: 0;
          opacity: 0;
          font-size: 18px;
          transform-origin: left center;
        }
      }

      .title {
        font-size: 36px;
        margin: 0;
        transform-origin: left center;
      }

      .btc {
        width: 100%;
        background: #fff;
        position: relative;
        z-index: 1;
        margin-top: 10px;

        .bg {
          position: absolute;
          top: 0;
          left: 0;
          right: 0;
          bottom: 0;
          background: #ffffff;
          opacity: 0;
          z-index: 1;
          transition: .2s;
        }

        img {
          max-width: 100%;
          transition: .2s;
        }
      }
    }
  }
</style>
