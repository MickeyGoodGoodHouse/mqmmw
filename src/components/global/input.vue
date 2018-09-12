<template>
  <div class="inputGroup" >
    <input :class="inputStyle" style="iStyle" @focus="inputFocus" @blur="inputBlur" />
    <button :v-if="showButton" :class="buttonStyle" @mousedown="onMousedown" @mouseup="onMouseup" >
      {{buttonText}}
    </button>
  </div>
</template>

<script>
export default {
  name: 'Input',
  props:{
    type:"",
    buttonText:"",
    iStyle:Object,
  },
  data () {
    return {
      showButton: this.type==="searchInput",
      buttonStyle:"button",
      inputStyle: this.type==="searchInput"?"searchInput":"normalInput",
    }
  },
  methods: {
    onMousedown () {
      this.buttonStyle="onMousedown";
    },
    onMouseup () {
      this.buttonStyle="onMouseup";
    },
    inputFocus () {
       this.buttonStyle="buttonFocus";
    },
    inputBlur () {
       this.buttonStyle="button";
    }
  }
}
</script>

<style lang="scss">
$colorBlue:rgb(24,169,255);
$colorWite: #FFF;
// $colorClick: #047796;
$colorDeepBlue:rgb(51, 133, 255);
@mixin inputBase{
    height: 30px;
    width: 400px;
    font-size: 17px;
    // padding-left: 8px;
    box-shadow: none;
    border-top-width: 2px;
    padding: 4px 15px;
    border: 1px rgb(200, 200, 200) solid;
    outline: none;
    vertical-align:bottom; 
    &:hover,
    &:focus {
        border: 1px $colorBlue solid;
    }
}
@mixin buttonBase{
    border: 0px;
    outline: none;
    font-size: 17px;
    padding: 0 15px;
    height: 40px;
    background-color:  $colorBlue;
    border-radius: 0px 5px 5px 0px;
    color: #FFF;
}
.inputGroup{
  font-size: 0px;
  height: 34px;
}
.normalInput {
   @include inputBase;
    border-radius: 5px;
}
.searchInput {
  @include inputBase;
  border-radius: 5px 0px 0px 5px;
}
.button {
  @include buttonBase;
}
.onMousedown{
   @include buttonBase;
  animation:onMousedown 0.5s 1;
  animation-fill-mode: forwards;
}
.onMouseup{
  @include buttonBase;
  animation:onMouseup 0.5s 1;
}
.buttonFocus{
  @include buttonBase;
  box-shadow:0 0 10px rgb(24,169,255);
}
@keyframes onMousedown {
  from {
    background-color: $colorBlue;
  };
  to {
    background-color:$colorDeepBlue;
  }
}
@keyframes onMouseup {
  from {
    background-color: $colorDeepBlue;
  };
  to {
    background-color: $colorBlue;
  }
}
</style>
