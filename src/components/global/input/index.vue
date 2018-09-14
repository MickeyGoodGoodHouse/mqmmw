<template>
  <span class="inputComponents" >
    <input
      :class="inputStyle"
      ref="input"
      :placeholder="placeholder"
      :value="value"
      :style="iStyle"
      :disabled="inputEdit==='disabled'"
      :readonly="inputEdit==='readonly'"
      @change="getValue"
      @blur="focusState = false"
      v-focus="focusState"
    />
    <span>
    <button
      v-if="showButton"
      :class="buttonStyle"
      @mousedown="mousedownButton"
      @mouseup="mouseupButton"
      @click="onClickButton"
    >
      {{buttonText}}
    </button>
    </span>
  </span>
</template>

<script>
export default {
  name: 'Input',
  props:{
    type:"",
    buttonText:"",
    iStyle:Object,
    placeholder:"",
    onClick:Function,
    defaultValue:"",
    inputEdit:"edit",
  },
  data () {
    return {
      showButton: this.type==="searchInput"?true:false,
      buttonStyle:"button",
      inputStyle: "normalInput",
      focusState: false,
      value:this.defaultValue,
    }
  },
  directives: {
    focus: {
      update: function (el, {value}) {
        if (value) {
          el.focus()
        }
      }
    }
  },
  methods: {
    onClickButton () {
      this.onClick(this);
    },
    getValue(value){
      this.value = value.target.value;
    },
    mousedownButton () {
      this.inputStyle = "mousedownInput";
      this.buttonStyle="mousedownButton";
    },
    mouseupButton () {
      this.focusState = true;
      this.inputStyle = "mouseupInput";
      this.buttonStyle="mouseupButton";
    },
    // inputFocus () {
    //    this.buttonStyle="buttonFocus";
    // },
    // inputBlur () {
    //    this.buttonStyle="button";
    // }
  }
}
</script>

<style lang="scss">
$colorBlue: rgb(24, 169, 255);
$colorWite: #fff;
$colorGary: rgb(200, 200, 200);
$colorDeepBlue: rgb(51, 133, 255);
$buttonShadowColor: rgba(51, 133, 255, 0.3);
@mixin inputBase {
    height: 30px;
    width: calc(100% - 32px);
    font-size: 17px;
    // padding-left: 8px;
    box-shadow: none;
    border-top-width: 2px;
    padding: 4px 15px;
    border-radius: 5px;
    border: 1px $colorGary solid;
    outline: none;
    vertical-align: bottom;
    &:hover,
    &:focus {
        border: 1px $colorBlue solid;
    }
    &:focus {
        box-shadow: 0 0 5px $colorBlue;
    }
}
@mixin buttonBase {
    border: 0px;
    outline: none;
    font-size: 17px;
    padding: 0 15px;
    height: 40px;
    background-color: $colorBlue;
    border-radius: 0px 5px 5px 0px;
    color: $colorWite;
    position: absolute;
    top: 0px;
    right: 0px;
}
.inputComponents {
    font-size: 0px;
    height: 34px;
    position: relative;
    width: 100%;
    display: inline-block;
}
.normalInput {
    @include inputBase;
}
.mouseupInput {
    @include inputBase;
    animation: mouseupInputShadow 0.8s 1;
}
.mousedownInput {
    @include inputBase;
    animation: mousedownInputShadow 0.8s 1;
    animation-fill-mode: forwards;
    border: 1px $colorBlue solid;
}
.button {
    @include buttonBase;
}
.mousedownButton {
    @include buttonBase;
    animation: mousedownButton 0.3s 1;
    animation-fill-mode: forwards;
}
.mouseupButton {
    @include buttonBase;
    animation: mouseupButton 0.3s 1;
}
@keyframes mousedownInputShadow {
    from {
        box-shadow: 0 0 5px $colorBlue;
    }
    to {
        box-shadow: none;
    }
}
@keyframes mouseupInputShadow {
    from {
        font-size: 17px;
    }
    to {
        box-shadow: 0 0 5px $colorBlue;
    }
}
@keyframes mousedownButton {
    from {
        background-color: $colorBlue;
    }
    to {
        background-color: $colorDeepBlue;
    }
}
@keyframes mouseupButton {
    from {
        background-color: $colorDeepBlue;
    }
    to {
        background-color: $colorBlue;
        box-shadow: 0 0 0 5px $buttonShadowColor;
    }
}
</style>
