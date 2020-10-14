<template>
  <div class="hello">
    <div id = "score">
      <h3>
        <img class="mini avatar" src = "../assets/流川.jpeg" :class = "{active: player == 0}"/>
        投{{balls[0]}}中{{score[0] / 2}}: {{score[0]}}分
        <br/>
        <img class="mini avatar" src = "../assets/櫻木.jpeg" :class = "{active: player == 1}" />
        投{{balls[1]}}中{{score[1] / 2}}: {{score[1]}}分
      </h3>
    </div>
    <div id = "dunk" v-if = "showDunk">
      <img id = "d0" v-show = "player == 0" class="d" src="../assets/流川灌籃.jpeg">
      <img id = "d1" v-show = "player == 1" class="d" src="../assets/櫻木灌籃.jpeg">
    </div>
    <div id = "basket" v-show = "!showDunk">
      <img id = "b" src="../assets/basket.jpg" />
    </div>
    <div id = "ball" v-show = "!showDunk">
      <img src="../assets/ball.png" :style = "{top: dy + 'px', left:dx +'px', transform: 'scale(' + size +')'}" :class = "{shoot: sh}" @click = "stop()"/>
    </div>
    <img class="big right avatar" src = "../assets/流川.jpeg" :class = "{active: player == 0}"/>
    <img class="big left avatar" src = "../assets/櫻木.jpeg" :class = "{active: player == 1}" />
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
      player: 0,
      size: 1,
      dx: 0,
      dy: 0,
      showDunk: false,
      xS: true,
      yX: true,
      xM: 1,
      yM: 0,
      win: false,
      sh: false,
      balls: [0,0],
      score: [0,0]
    }
  },
  methods: {
    keydown (e) {
      console.log('keydown');
      if (e.which == 32) {
        this.stop()
      }
      if (e.which == 13) {
        this.dunk()
      }
    },
    part() {
      this.dy += 15;
    },
    animate() {
      this.size = 1;
      this.dy += 15;
      this.balls[this.player] += 1;
      console.log('shoot')
      if (Math.abs(this.dx) ** 2 + Math.abs(this.dy) ** 2 <= 1000) {
        console.log('win!')  
        this.win = true,
        this.score[this.player] += 2;
      } else {
        /* */
      }
      this.xM = 1
      this.yM = 0
      this.sh = false
      this.player = 1 - this.player
    },
    shoot() {
      this.size = 0.5;
      this.dy -= 30;
      this.sh = true;
      setTimeout(this.part, 500);
      setTimeout(this.animate, 1000);
    },
    dunk() {
      this.showDunk = true;
      this.balls[this.player] += 1;
      console.log('dunk!')  
      this.win = true,
      this.score[this.player] += 2;
      this.xM = 1
      this.yM = 0
      this.sh = false
      setTimeout(this.dunkEnd, 1000)
    },
    dunkEnd() {
      this.showDunk = false
      this.player = 1 - this.player
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
    window.addEventListener('keydown', this.keydown)
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

#basket, #ball, #dunk {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}

#ball img, #dunk img {
  position: relative;
}

#ball img {
  width: 100px;
}

#dunk img {
  width: 100%;
}

#ball img.shoot {
  transition: all 0.5s ease;
}

.mini.avatar {
  height: 1em;
}

.big.avatar {
  position: fixed;
  bottom: 0;
  width: 25vw;
}

.right {
  right: 0;
}

.left {
  left: 0;
}

.active.avatar {
  border: 5px ridge gold;
}

</style>
