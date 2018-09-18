<template>
  <div class="bannerComponents" >
    <div :class="typeof(scrolled)==='boolean' ? (scrolled? 'bannerComponentsFlip' : 'bannerComponentsFlipBack'):''" >
      <div>
        <img src="@/assets/favicon.png" alt="LOGO" class="logo">
        <span class="webName" >Mickey Fantasy House</span>
        <span class ="bannerSearchBar">
            <img src="@/assets/search.png" alt="search" class="searchIcon" >
            <input class="bannerInput" :placeholder="placeholder" />
        </span>
      </div>
      <div class = "underBanner" >
        <img src="@/assets/favicon.png" alt="LOGO" class="logo">
        <span class="webName" >Mickey Fantasy House</span>
      <!-- <span class ="bannerSearchBar">
        <img src="@/assets/search.png" alt="search" class="searchIcon" >
        <input class="bannerInput" :placeholder="placeholder" />
      </span> -->
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
  },
  data () {
    return {
      placeholder:"不来Gay一下吗",
    }
  },
  methods: {
    
  },
}
</script>

<style lang="scss">
.underBanner {
    transform: rotateX(-90deg) translateZ(-25px);
}
.bannerComponents {
    background-color: white;
    position: fixed;
    width: 100%;
    z-index: 99;
    overflow: hidden;
    text-align: left;
    height: 50px;
    margin-bottom: 50px;
    padding-left: 40px;
    padding-top: 6px;
    padding-bottom: 6px;
    box-shadow: 0 0 20px rgb(235, 235, 235);
    transition: all 2s;
    &:hover {
        height: 500px;
    }
}
.bannerComponentsFlip {
    animation: Flip 1s 1;
    animation-fill-mode: forwards;
    transform-style: preserve-3d;            // 使子元素保留其3D视角
}
.bannerComponentsFlipBack {
    animation: FlipBack 1s 1;
    animation-fill-mode: forwards;
    transform-style: preserve-3d;            // 使子元素保留其3D视角
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
}
.bannerSearchBar {
    padding-left: 130px;
    display: inline-block;
    vertical-align: middle;
    @media screen and (max-width: 744px) {
        padding-left: 0px;
    }
}
.searchIcon {
    height: 26px;
    vertical-align: middle;
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
        transform-origin: 25px 25px;
        transform:rotateX(0deg);
    }
    to {
        transform-origin: 25px 25px;
        // transform-origin : 00% 0% 50%;
        transform:rotateX(90deg);
    }
}
@keyframes FlipBack {
    from {
        transform-origin: 25px 25px;
        transform:rotateX(90deg);
    }
    to {
        transform-origin: 25px 25px;
        // transform-origin : 00% 0% 50%;
        transform:rotateX(0deg);
    }
}
</style>
