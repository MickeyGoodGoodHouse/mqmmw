<template>
<div class="spinComponents">
  <div v-if="spining" class="cover" >
    <div class="spinComponentsItem" >
      <div class="spinUpperLeft" ></div>
      <div class="spinUpperRight" ></div>
      <div class="spinLowerLeft" ></div>
      <div class="spinlowerRight" ></div>
    </div>  
  </div>
  <slot></slot> 
</div>
</template>

<script>

export default {
  name: 'spin',
  props:{
    spining:true,
  },
  data () {
    return {
    }
  },
  methods: {
    
  }
}
</script>

<style lang="scss">
$leftBollColor: rgb(17, 85, 114);
$rightBollColor: rgb(215, 59, 39);
$ballShadow: rgba(204, 204, 204, 0.6);
@mixin spin {
    width: 15px;
    height: 15px;
}
.spinComponents {
    position: relative;
}
.cover {
    background-color: rgba(255, 255, 255, 0.5);
    height: 100%;
    position: absolute;
    line-height: 500px;
    width: 100%;
    vertical-align: middle;
    z-index: 99;
}
// @mixin ball {
//     width: 26px;
//     height: 26px;
//     border-radius: 50%;
//     display: inline-block;
// }
// @mixin shadow {
//     width: 26px;
//     height: 26px;
//     border-radius: 50%;
//     display: inline-block;
//     background-color: $ballShadow;
//     transform: rotateX(75deg);
// }
.spinComponentsItem {
    font-size: 0px;
    width: 40px;
    line-height: 0px;
    display: inline-block;
    animation: rotate 1s linear infinite;
}
// .spinComponentsTwo {
//     font-size: 0px;
//     text-align: center;
// }
.spinUpperLeft {
    @include spin;
    margin-bottom: 2px;
    margin-right: 2px;
    border-radius: 50% 50% 0 50%;
    display: inline-block;
    background-color: rgba(189, 102, 240, 0.664);
}
.spinUpperRight {
    @include spin;
    border-radius: 50% 50% 50% 0;
    display: inline-block;
    margin-bottom: 2px;
    background-color: rgba(213, 245, 73, 0.835);
}
.spinLowerLeft {
    @include spin;
    margin-right: 2px;
    border-radius: 50% 0 50% 50%;
    display: inline-block;
    background-color: rgba(240, 117, 35, 0.664);
}
.spinlowerRight {
    @include spin;
    border-radius: 0 50% 50% 50%;
    display: inline-block;
    background-color: rgba(102, 189, 240, 0.664);
}
// .ball {
//     margin-bottom: 20px;
// }
// .moveBallLeft {
//     @include ball;
//     background: $leftBollColor;
//     animation: ballUp 2s linear infinite;
//     animation-direction: alternate;
//     animation-timing-function: ease-out;
// }
// .moveBallRight {
//     @include ball;
//     background: $rightBollColor;
//     animation: ballDown 2s linear infinite;
//     animation-direction: alternate;
//     animation-delay: 2s;
//     animation-timing-function: ease-out;
// }
// .firstBall {
//     @include ball;
//     background: linear-gradient(
//         to right,
//         $leftBollColor,
//         ($rightBollColor - $leftBollColor) * 1/5 + $leftBollColor
//     );
// }
// .secondBall {
//     @include ball;
//     background: linear-gradient(
//         to right,
//         ($rightBollColor - $leftBollColor) * 1/5 + $leftBollColor,
//         ($rightBollColor - $leftBollColor) * 2/5 + $leftBollColor
//     );
// }
// .thirdBall {
//     @include ball;
//     background: linear-gradient(
//         to right,
//         ($rightBollColor - $leftBollColor) * 2/5 + $leftBollColor,
//         ($rightBollColor - $leftBollColor) * 3/5 + $leftBollColor
//     );
// }
// .fourthBall {
//     @include ball;
//     background: linear-gradient(
//         to right,
//         ($rightBollColor - $leftBollColor) * 3/5 + $leftBollColor,
//         ($rightBollColor - $leftBollColor) * 4/5 + $leftBollColor
//     );
// }
// .fifthBall {
//     @include ball;
//     background: linear-gradient(
//         to right,
//         ($rightBollColor - $leftBollColor) * 4/5 + $leftBollColor,
//         $rightBollColor
//     );
// }
// .moveShadowLeft {
//     @include shadow();
//     position: relative;
//     animation: shadowLeft 2s linear infinite;
//     animation-direction: alternate;
//     animation-timing-function: ease-out;
// }
// .moveShadowRight {
//     @include shadow();
//     position: relative;
//     animation: shadowRight 2s linear infinite;
//     animation-direction: alternate;
//     animation-delay: 2s;
//     animation-timing-function: ease-out;
// }
// .shadow {
//     @include shadow();
// }
@keyframes rotate {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(359deg);
    }
}
// @keyframes ballUp {
//     0% {
//         transform: rotate(0deg);
//         transform-origin: 0 -30px;
//     }
//     50% {
//         transform: rotate(0deg);
//         transform-origin: 0 -30px;
//     }
//     100% {
//         transform: rotate(90deg);
//         transform-origin: 0 -30px;
//     }
// }
// @keyframes ballDown {
//     0% {
//     }
//     50% {
//         transform: rotate(0deg);
//         transform-origin: 26px -30px;
//     }
//     100% {
//         transform: rotate(-90deg);
//         transform-origin: 26px -30px;
//     }
// }
// @keyframes shadowLeft {
//     0% {
//     }
//     50% {
//         left: 0px;
//         opacity: 1;
//     }
//     100% {
//         left: -65px;
//         opacity: 0;
//     }
// }
// @keyframes shadowRight {
//     0% {
//     }
//     50% {
//         left: 0px;
//         opacity: 1;
//     }
//     100% {
//         left: 70px;
//         opacity: 0;
//     }
// }
</style>
