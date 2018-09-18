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
      @keyup.enter="onClickButton"
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
    buttonType:String,
  },
  data () {
    return {
      showButton: this.type==="searchInput"?true:false,
      buttonStyle:this.buttonType&&this.buttonType==="primary"?"primary":"default",
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
      if(this.buttonType&&this.buttonType==="primary"){
        this.buttonStyle="primary primaryMousedown";
      }else{
        this.buttonStyle="default defaultMousedown";
      }
    },
    mouseupButton () {
      this.focusState = true;
      this.inputStyle = "mouseupInput";
      if(this.buttonType&&this.buttonType==="primary"){
        this.buttonStyle="primary primaryMouseup";
      }else{
        this.buttonStyle="default defaultMouseup";
      }
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
    border-radius: 0px 5px 5px 0px;
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
.primary {
    @include buttonBase;
    background-color: $colorBlue;
    color: $colorWite;
}
.default {
    @include buttonBase;
    background-color: $colorWite;
    color: $colorBlue;
    border: 1px $colorBlue solid;
}
.primaryMousedown {
    animation: primaryMousedown 0.3s 1;
    animation-fill-mode: forwards;
}
.defaultMousedown {
    animation: defaultMousedown 0.3s 1;
    animation-fill-mode: forwards;
}
.defaultMouseup {
    animation: defaultMouseup 0.3s 1;
}
.primaryMouseup {
    animation: primaryMouseup 0.3s 1;
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
@keyframes defaultMousedown {
    from {
        background-color: $colorWite;
        color: $colorBlue;
    }
    to {
        background-color: $colorBlue;
        color: $colorWite;
    }
}
@keyframes defaultMouseup {
    from {
        background-color: $colorBlue;
        color: $colorWite;
    }
    to {
        background-color: $colorWite;
        color: $colorBlue;
        box-shadow: 0 0 0 5px $buttonShadowColor;
    }
}
@keyframes primaryMousedown {
    from {
        background-color: $colorBlue;
    }
    to {
        background-color: $colorDeepBlue;
    }
}
@keyframes primaryMouseup {
    from {
        background-color: $colorDeepBlue;
    }
    to {
        background-color: $colorBlue;
        box-shadow: 0 0 0 5px $buttonShadowColor;
    }
}
</style>
