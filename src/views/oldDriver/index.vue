<template>
  <div>
    <Input buttonText="嘀嘀嘀，开车啦" type="searchInput" />
  </div>
</template>

<script>
import Input from "@/components/global/input.vue";
export default {
    name: "Header",
    components: {
        Input: Input,
    },
    data() {
        return {
        };
    }
};
</script>

<style lang="scss">
</style>