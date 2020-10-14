<template>
  <div class="hello">
    <div id = "score">
      <h1>投{{balls}}中{{score / 2}}: 得了{{score}}分</h1>
    </div>
    <div id = "basket">
      <img id = "b" src="../assets/basket.jpg" />
    </div>
    <div id = "ball">
      <img src="../assets/ball.png" :style = "{top: dy + 'px', left:dx +'px', transform: 'scale(' + size +')'}" :class = "{shoot: sh}" @click = "stop()"/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data () {
    return {
      size: 1,
      dx: 0,
      dy: 0,
      xS: true,
      yX: true,
      xM: 1,
      yM: 0,
      win: false,
      sh: false,
      balls: 0,
      score: 0
    }
  },
  methods: {
    part() {
      this.dy += 15;
    },
    animate() {
      this.size = 1;
      this.dy += 15;
      this.balls += 1;
      console.log('shoot')
      if (Math.abs(this.dx) ** 2 + Math.abs(this.dy) ** 2 <= 1000) {
        console.log('win!')  
        this.win = true,
        this.score += 2;
      } else {
        /* */
      }
      this.xM = 1
      this.yM = 0
      this.sh = false
    },
    shoot() {
      this.size = 0.5;
      this.dy -= 30;
      this.sh = true;
      setTimeout(this.part, 500);
      setTimeout(this.animate, 1000);
    },
    stop() {
      if (this.yM > 0) {
        this.yM = 0
        this.shoot()
      } else {
        if (this.xM > 0) {
          this.xM = 0
          this.yM = 1
        }
      }
    },
    moveX () {
      if (this.xS) {
        this.dx += this.xM
      } else {
        this.dx -= this.xM
      }
      if (Math.abs(this.dx) >= 100) {
        this.xS = !this.xS
      }
    },
    moveY () {
      if (this.yS) {
        this.dy += this.yM
      } else {
        this.dy -= this.yM
      }
      if (Math.abs(this.dy) >= 100) {
        this.yS = !this.yS
      }
    }
  },
  mounted () {
    setInterval(this.moveX, 5)
    setInterval(this.moveY, 5)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

#score {
  position: relative;
  z-index: 9;
}

#b {
  width: 33vw;
}

@media screen and (max-width: 600px) {
  #b {
    width: 100vw;
  }
}

#basket, #ball {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

#ball img {
  position: relative;
  width: 100px;
}

#ball img.shoot {
  transition: all 0.5s ease;
}

</style>
