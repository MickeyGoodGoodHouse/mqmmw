<template>
  <div class="bannerComponents" >
    <div :class="typeof(scrolled)==='boolean' ? (scrolled? 'bannerComponentsFlip' : 'bannerComponentsFlipBack'):''" >
      <div class="topBanner" >
        <span>
          <img src="static/logo.png" alt="LOGO" class="logo">
          <span class="webName" >Mickey Fantasy House</span>
        </span>
        <span v-if="isPC" class ="bannerSearchBar">
            <img src="static/search.png" alt="search" class="searchIcon" >
            <input class="bannerInput" :placeholder="placeholder" />
        </span>
        <span v-if="isPC" >
          <img src="static/bell.png" alt="bell" class="leftIcon" >
          <img src="static/talk.png" alt="talk" class="leftIcon" >
          <img src="static/userHead.png" alt="userHead" class="userHead" >
        </span>
      </div>
      <div class = "underBanner" >
        <span>
          <img :src="modulesIcon" alt="LOGO" class="logo">
          <span class="webName" >{{modulesName}}</span>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import Input from "@/components/global/input";
export default {
  name: 'banner',
  components: {
        Input: Input,
    },
  props:{
    scrolled:Boolean,
    modulesName:String,
    modulesIcon:String,
    titleText:String,
  },
  data () {
    return {
      placeholder:"不来Gay一下吗",
      isPC:true,
    }
  },
  created:function(){
    if (/(iPhone|iPad|iPod|iOS|Android)/i.test(navigator.userAgent)) {
      this.isPC = false;
    }else{
      this.isPC = true;
    }
  },
  methods: {
    
  },
}
</script>

<style lang="scss">
@mixin icon {
    height: 26px;
    vertical-align: middle;
}
.topBanner {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.underBanner {
    @extend .topBanner;
    transform: rotateX(90deg) translateZ(25px) translateY(25px);
}
.bannerComponents {
    background-color: white;
    position: fixed;
    width: calc(100% - 80px);
    z-index: 100;
    overflow: hidden;
    text-align: left;
    height: 50px;
    margin-bottom: 50px;
    padding-left: 40px;
    padding-right: 40px;
    padding-top: 6px;
    padding-bottom: 6px;
    box-shadow: 0 0 20px rgb(235, 235, 235);
    transition: all 1s;
    &:hover {
        height: 500px;
    }
}
.bannerComponentsFlip {
    animation: Flip 0.5s 1;
    animation-fill-mode: forwards;
    transform-style: preserve-3d;
}
.bannerComponentsFlipBack {
    animation: FlipBack 0.5s 1;
    animation-fill-mode: forwards;
    transform-style: preserve-3d;
}
.logo {
    height: 50px;
    display: inline-block;
    vertical-align: middle;
}
.webName {
    user-select: none;
    font-size: 18px;
    padding-left: 10px;
    font-weight: bold;
    vertical-align: middle;
}
.bannerSearchBar {
    display: inline-block;
    vertical-align: middle;
    @media screen and (max-width: 744px) {
        padding-left: 0px;
    }
}
.searchIcon {
    @include icon;
}
.leftIcon {
    @include icon;
    margin-right: 30px;
}
.userHead {
    width: 50px;
    height: 50px;
    vertical-align: middle;
    border-radius: 50%;
}
.bannerInput {
    vertical-align: middle;
    outline: none;
    line-height: 18px;
    border: none;
    width: 178px;
    height: 24px;
    font-size: 18px;
    padding: 4px 11px;
}
@keyframes Flip {
    from {
        transform-origin: 25px 0px;
        transform: rotateX(0deg);
    }
    to {
        transform-origin: 25px 0px;
        transform: rotateX(-90deg);
    }
}
@keyframes FlipBack {
    from {
        transform-origin: 25px 0px;
        transform: rotateX(-90deg);
    }
    to {
        transform-origin: 25px 0px;
        transform: rotateX(0deg);
    }
}
</style>
