<template>
  <div class="wrapper" ref="scroll">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from "@better-scroll/core";
import Pullup from "@better-scroll/pull-up";
import PullDown from "@better-scroll/pull-down";

BScroll.use(Pullup);
BScroll.use(PullDown);

export default {
  name: "Scroll",
  data() {
    return {
      isPullUpLoad: false,
    };
  },
  methods: {
    initBscroll() {
      this.bscroll = new BScroll(this.$refs.scroll, {
        probeType: 3,
        pullUpLoad: true,
      });
      this.bscroll.on("scroll", (position) => {
        console.log(position);
      });
      this.bscroll.on("pullingUp", this.pullingUpHandler);
    },
    pullingUpHandler() {
      this.isPullUpLoad = true;

      this.bscroll.finishPullUp();

      this.isPullUpLoad = false;
    },
  },
  mounted() {
    this.initBscroll();
  },
};
</script>

<style scoped>
</style>
