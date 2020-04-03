<template>
  <div class="layout">
    <canvas id="canvas"></canvas>
    <div id="corners">
      <img src="../assets/corner-tl.png" id="corner-tl">
      <img src="../assets/corner-tr.png" id="corner-tr">
      <img src="../assets/corner-bl.png" id="corner-bl">
      <img src="../assets/corner-br.png" id="corner-br">
      <div id="lines">
        <span id="top-line"></span>
        <span id="bottom-line"></span>
        <span id="left-line"></span>
        <span id="right-line"></span>
      </div>
    </div>
    <div id="header">
        <div id="nav-links">
            <a href="/" @mouseover="isHovering1 = true" 
                @mouseout="isHovering1 = false" 
                :class="{hovering: isHovering1}">
                Home<span></span>
            </a>
            <a href="/" @mouseover="isHovering2 = true" 
                @mouseout="isHovering2 = false" 
                :class="{hovering: isHovering2}">
                Skills<span></span>
            </a>
            <a href="/" @mouseover="isHovering3 = true" 
                @mouseout="isHovering3 = false" 
                :class="{hovering: isHovering3}">
                Work<span></span>
            </a>
            <a href="/" @mouseover="isHovering4 = true" 
                @mouseout="isHovering4 = false" 
                :class="{hovering: isHovering4}">
                Contact<span></span>
            </a>
        </div>
    </div>
    <Mainsection />
    <div id="footer"><p>Copyright © {{ new Date().getFullYear() }} Jack Gugi</p></div>
  </div>
</template>


<script>
import Mainsection from './Mainsection'

export default {
  name: 'Layout',
  components: {
    Mainsection
  },
  data() {
    return {
      pagTitle: 'Mainsection',
      logo: './assets/logo.png',
      isHovering1: false,
      isHovering2: false,
      isHovering3: false,
      isHovering4: false
    }
  },
  methods: {
    
  },
  mounted () {
    var canvas = document.getElementById("canvas"),
    ctx = canvas.getContext("2d"),
    w = (canvas.width = window.innerWidth),
    h = (canvas.height = window.innerHeight),
    hue = 253,
    stars = [],
    count = 0,
    maxStars = 1400;

    var canvas2 = document.createElement("canvas"),
    ctx2 = canvas2.getContext("2d");
    canvas2.width = 100;
    canvas2.height = 100;
    var half = canvas2.width / 2,
    gradient2 = ctx2.createRadialGradient(half, half, 0, half, half, half);
    gradient2.addColorStop(0.025, "#fff");
    gradient2.addColorStop(0.1, "hsl(" + hue + ", 71%, 13%)");
    gradient2.addColorStop(0.25, "hsl(" + hue + ", 52%, 3%)");
    gradient2.addColorStop(1, "transparent");

    ctx2.fillStyle = gradient2;
    ctx2.beginPath();
    ctx2.arc(half, half, half, 0, Math.PI * 3);
    ctx2.fill();

    // End cache

    function random(min, max) {
    if (arguments.length < 2) {
        max = min;
        min = 0;
    }

    if (min > max) {
        var hold = max;
        max = min;
        min = hold;
    }

    return Math.floor(Math.random() * (max - min + 1)) + min;
    }

    function maxOrbit(x, y) {
        var max = Math.max(x, y),
        diameter = Math.round(Math.sqrt(max * max + max * max));
        return diameter / 2;
    }

    var Star = function () {
        this.orbitRadius = random(maxOrbit(w, h));
        this.radius = random(60, this.orbitRadius) / 12;
        this.orbitX = w / 2;
        this.orbitY = h / 2;
        this.timePassed = random(0, maxStars);
        this.speed = random(this.orbitRadius) / 550000;
        this.alpha = random(2, 10) / 10;

        count++;
        stars[count] = this;
    };

    Star.prototype.draw = function () {
    var x = Math.sin(this.timePassed) * this.orbitRadius + this.orbitX,
        y = Math.cos(this.timePassed) * this.orbitRadius + this.orbitY,
        twinkle = random(10);

    if (twinkle === 1 && this.alpha > 0) {
        this.alpha -= 0.05;
    } else if (twinkle === 2 && this.alpha < 1) {
        this.alpha += 0.05;
    }

    ctx.globalAlpha = this.alpha;
    ctx.drawImage(
        canvas2,
        x - this.radius / 2,
        y - this.radius / 2,
        this.radius,
        this.radius
    );
    this.timePassed += this.speed;
    };

    for (var i = 0; i < maxStars; i++) {
    new Star();
    }

    function animation() {
    ctx.globalCompositeOperation = "source-over";
    ctx.globalAlpha = 0.8;
    ctx.fillStyle = "hsla(210, 40%, 2%, 1)";
    ctx.fillRect(0, 0, w, h);

    ctx.globalCompositeOperation = "lighter";
    for (var i = 1, l = stars.length; i < l; i++) {
        stars[i].draw();
    }

    window.requestAnimationFrame(animation);
    }

    animation();
  }
}
</script>


<style scoped>
.layout {
    position: relative;
}

#canvas {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}

#corners {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
}

#corners img {
    position: absolute;
    width: 30px;
}

#corner-tl {
    left: 20px;
    top: 20px;
}

#corner-tr {
    right: 20px;
    top: 20px;
}

#corner-bl {
    left: 20px;
    bottom: 20px;
}

#corner-br {
    right: 20px;
    bottom: 20px;
}

#lines {
    position: absolute;
    left: 20px;
    right: 20px;
    top: 20px;
    bottom: 20px;
    overflow: hidden;
}

@keyframes topLine {
    0%   {
        left: 0;
        transform: translateX(-100%);
    }
    80% {
        left: 100%;
        transform: translateX(0);
    }
    100% {
        left: 100%;
        transform: translateX(0);
    }
}

#top-line {
    display: block;
    position: absolute;
    top: 1px;
    height: 1px;
    width: 250px;
    background: #AFDACF;
    left: 0%;
    animation-name: topLine;
    animation-timing-function: ease;
    animation-duration: 13s;
    animation-iteration-count: infinite;
}

@keyframes bottomLine {
    0%   {
        right: 0;
        transform: translateX(100%);
    }
    2%   {
        right: 0;
        transform: translateX(100%);
    }
    80% {
        right: 100%;
        transform: translateX(0);
    }
    100% {
        right: 100%;
        transform: translateX(0);
    }
}

#bottom-line {
    display: block;
    position: absolute;
    bottom: 1px;
    height: 1px;
    width: 250px;
    background: #AFDACF;
    right: 0;
    animation-name: bottomLine;
    animation-timing-function: ease;
    animation-duration: 13s;
    animation-iteration-count: infinite;
}

@keyframes leftLine {
    0%   {
        bottom: 0;
        transform: translateY(100%);
    }
    60%   {
        bottom: 0;
        transform: translateY(100%);
    }
    100% {
        bottom: 100%;
        transform: translateY(0);
    }
}

#left-line {
    display: block;
    position: absolute;
    bottom: 0;
    width: 1px;
    height: 250px;
    background: #AFDACF;
    left: 1px;
    transform: translateY(100%);
    animation-name: leftLine;
    animation-timing-function: ease;
    animation-duration: 13s;
    animation-iteration-count: infinite;
}

@keyframes rightLine {
    0%   {
        top: 0;
        transform: translateY(-100%);
    }
    60%   {
        top: 0;
        transform: translateY(-100%);
    }
    100% {
        top: 100%;
        transform: translateY(0);
    }
}

#right-line {
    display: block;
    position: absolute;
    top: 0;
    width: 1px;
    height: 250px;
    background: #AFDACF;
    right: 1px;
    transform: translateY(100%);
    animation-name: rightLine;
    animation-timing-function: ease;
    animation-duration: 13s;
    animation-iteration-count: infinite;
}

#header {
    display: inline-block;
    margin-top: 45px;
    position: relative;
}

.mainsection {
    display: inline-block;
    width: 100%;
    position: relative;
    height: 540px;
    overflow: hidden;
    min-height: 90vh;
}

#nav-links a {
    color: #AFDACF;
    text-decoration: none;
    margin: 0 40px;
    letter-spacing: 0;
    text-transform: uppercase;
    font-size: 18px;
    position: relative;
    transition: 0.3s all;
    display: inline-block;
    font-family: 'ultraregular';
}

#nav-links a span {
    position: absolute;
    bottom: -18px;
    display: inline-block;
    height: 1px;
    width: 0;
    background: #fff;
    box-shadow: 0 0 13px #EDBCD1, 0 0 8px #E390BA, 0 0 5px #E390BA;
    left: 50%;
    opacity: 0;
    transition: 0.3s all ease-in-out;
}

#nav-links .hovering span {
    opacity: 1;
    left: 0;
    right: 10px;
    width: auto;
    transition: 0.3s all ease-in-out;
}

#nav-links .hovering {
    color: #fff;
    text-shadow: 0 0 20px #E390BA, 0 0 10px #E390BA, 0 0 5px #E390BA;
}
</style>
