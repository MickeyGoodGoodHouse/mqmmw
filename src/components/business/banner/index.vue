<template>
  <div class="bannerComponents" >
    <img src="@/assets/favicon.png" alt="LOGO" class="logo">
    <span class="webName" >Mickey Fantasy House</span>
    <span class ="bannerSearchBar">
      <img src="@/assets/search.png" alt="search" class="searchIcon" >
      <input class="bannerInput" :placeholder="placeholder" />
    </span>
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
  },
  data () {
    return {
      placeholder:"不来Gay一下吗",
    }
  },
  methods: {
    
  }
}
</script>

<style lang="scss">
.bannerComponents {
    text-align: left;
    margin-bottom: 50px;
    padding-left: 40px;
    padding-top: 5px;
    padding-bottom: 5px;
    box-shadow: 0 0 20px rgb(235, 235, 235);
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
</style>
