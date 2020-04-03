<template>
  <div class="mainsection" v-on:mousemove="updateCoordinates">
    <div id="brush">
      <div id="circ1wrap">
        <img src="../assets/circle1.png" id="circle1">
      </div>
      <div id="circ2wrap">
        <div id="circ2inner">
          <img src="../assets/circle2.png" id="circle2">
        </div>
      </div>
      <div id="circ3wrap">
        <div id="circ3inner">
          <img src="../assets/circle3.png" id="circle3" v-on:click="spinCircle">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// export default {
//   name: 'MyList',
//   data() {
//     return {
//       pagTitle: 'Favourite Foods',
//       sausages: 'Add a new food',
//       showing: true,
//       foods: [
//         {foodId: 'p', foodName: 'Pizza'},
//         {foodId: 'b', foodName: 'Burger'},
//         {foodId: 'l', foodName: 'Lasagne'}
//       ]
//     }
//   },
//   methods: {
//     addNewFood: function() {
//       this.foods.push({foodId: 'c', foodName: this.sausages})
//     }
//   }
// }

export default {
  name: 'Mainsection',
  data() {
    return {
      pagTitle: 'Welcome',
      x: 0,
      y: 0,
      rotateVal: 0
    }
  },
  methods: {
    updateCoordinates: function(event) {
      // pass event object, bound to mouse move with update
      this.x = event.clientX;
      this.y = event.clientY;
      // this.rotateVal = (this.x - this.y) / 10;

      // document.getElementById('circ2wrap').style.transform = 'rotate3d(1, 1, 0, ' + this.rotateVal + 'deg)';

      var rotateForce = 25; // max rotation in deg
      
      var docX = window.innerWidth;
      var docY = window.innerHeight;
    
      var rotateY = (this.x / docX * rotateForce*2) - rotateForce;
      var rotateX = -((this.y / docY * rotateForce*2) - rotateForce);
      document.getElementById('circ2wrap').style.transform = 'rotateX('+rotateX+'deg) rotateY('+rotateY+'deg)';
    },
    spinCircle: function() {
      var circle1 = document.getElementById('circ1wrap');
      var circle2 = document.getElementById('circ2inner');
      var circle3 = document.getElementById('circ3wrap');
      var circle3wrap = document.getElementById('circ3inner');
      circle1.classList.add("spinCircle");
      circle2.classList.add("spinReverse");
      circle3.classList.add("spinPowerSource");
      circle3wrap.classList.add("increaseWidth");
      
      setTimeout(function(){ 
        circle1.classList.remove("spinCircle");
        circle2.classList.remove("spinReverse");
        circle3.classList.remove("spinPowerSource");
        circle3wrap.classList.remove("increaseWidth");
      }, 8000);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  margin: 40px 0 0;
  color: #fff;
}

.mainsection {
    display: inline-block;
    min-height: 800px;
    width: 100%;
    perspective: 800px;
}

#brush {
    /* opacity: 0; */
    transition: 1s all ease-in-out;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: auto;
    transform-style: preserve-3d;
}

#circ1wrap, #circ2wrap, #circ3wrap {
    transition-timing-function: ease-in-out;
}

@keyframes rotateCircle {
  from {
    transform: translate(-50%, -50%) rotate(0deg);
  }
  to {
    transform: translate(-50%, -50%) rotate(360deg);
  }
}

@keyframes rotateOuter {
  from {
    transform: translate(-50%, -50%) rotate(0deg);
  }
  to {
    transform: translate(-50%, -50%) rotate(-360deg);
  }
}

@keyframes rotateInner {
  0% {
    transform: translate(-50%, -50%) rotate(0deg);
  }
  10% {
    filter: brightness(2);
  }
  20% {
    filter: brightness(1);
  }
  30% {
    filter: brightness(2);
  }
  40% {
    filter: brightness(1);
  }
  50% {
    filter: brightness(2);
  }
  60% {
    filter: brightness(1);
  }
  70% {
    filter: brightness(2);
  }
  80% {
    filter: brightness(1);
  }
  90% {
    filter: brightness(2);
  }
  100% {
    transform: translate(-50%, -50%) rotate(-360deg);
    filter: brightness(1);
  }
}

#circle1 {
  width: 300px;
  height: 300px;
  position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
  animation-name: rotateCircle;
  animation-timing-function: linear;
  animation-duration: 120s;
  animation-iteration-count: infinite;
}

#circle2 {
    width: 490px;
    height: 490px;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    animation-name: rotateOuter;
    animation-timing-function: linear;
    animation-duration: 190s;
    animation-iteration-count: infinite;
}

#circle3 {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 100%;
  animation-name: rotateInner;
  animation-timing-function: linear;
  animation-duration: 9s;
  animation-iteration-count: infinite;
  cursor: pointer;
}

#circ3inner {
  width: 66px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

@keyframes spinCircle {
  0% {
    transform: translate(-50%, -50%) rotate(0deg);
  }
  100% {
    transform: translate(-50%, -50%) rotate(3600deg);
  }
}

.spinCircle {
  animation-name: spinCircle;
  animation-duration: 8s;
  animation-timing-function: ease-in-out;
}

@keyframes spinReverse {
  0% {
    transform: translate(-50%, -50%) rotate(0deg);
  }
  100% {
    transform: translate(-50%, -50%) rotate(-1080deg);
  }
}

.spinReverse {
  animation-duration: 8s;
  animation-name: spinReverse;
  animation-timing-function: ease-in-out;
}

@keyframes spinPowerSource {
  0% {
    transform: translate(-50%, -50%) rotate(0deg);
  }
  100% {
    transform: translate(-50%, -50%) rotate(-2880deg);
  }
}

.spinPowerSource {
  animation-duration: 8s;
  animation-name: spinPowerSource;
  animation-timing-function: ease-in-out;
}

@keyframes increaseWidth {
  0% { width: 66px; filter: brightness(1);}
  10% { width: 85px; filter: brightness(2); }
  20% { width: 66px; filter: brightness(1); }
  25% { width: 85px; filter: brightness(2); }
  30% { width: 66px; filter: brightness(1); }
  35% { width: 85px; filter: brightness(2); }
  40% { width: 66px; filter: brightness(1); }
  45% { width: 85px; filter: brightness(2); }
  50% { width: 66px; filter: brightness(1); }
  55% { width: 85px; filter: brightness(2); }
  60% { width: 66px; filter: brightness(1); }
  65% { width: 85px; filter: brightness(2); }
  70% { width: 66px; filter: brightness(1); }
  75% { width: 85px; filter: brightness(2); }
  80% { width: 66px; filter: brightness(1); }
  90% { width: 85px; filter: brightness(2); }
  100% { width: 66px; filter: brightness(1); }
}

.increaseWidth {
  animation-duration: 8s;
  animation-name: increaseWidth;
  animation-timing-function: ease-in-out;
}
</style>
