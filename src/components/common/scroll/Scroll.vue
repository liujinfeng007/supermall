<template>
  <div class="wrapper" ref="bscroll">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from "@better-scroll/core";
import Pullup from "@better-scroll/pull-up";
import PullDown from "@better-scroll/pull-down";
import ObserveImage from "@better-scroll/observe-image";

BScroll.use(Pullup);
BScroll.use(PullDown);
BScroll.use(ObserveImage);

export default {
  name: "Scroll",
  props: { probeType: { type: Number, default: 0 } },
  data() {
    return {
      bscroll: null,
      isPullUpLoad: false,
    };
  },
  methods: {
    initBscroll() {
      this.bscroll = new BScroll(this.$refs.bscroll, {
        probeType: this.probeType,
        click: true,
        pullUpLoad: true,
        observeImage: true,
      });
      this.bscroll.on("scroll", (position) => {
        this.$emit("scroll", position);
      });
      this.bscroll.on("pullingUp", this.pullingUpHandler);
    },
    pullingUpHandler() {
      this.isPullUpLoad = true;

      this.$emit("pullingUp");
      this.bscroll.finishPullUp();

      this.bscroll.refresh();

      this.isPullUpLoad = false;
    },
    scrollTo(x, y, time = 500) {
      this.bscroll.scrollTo(x, y, time);
    },
  },
  mounted() {
    this.initBscroll();
  },
};
</script>

<style scoped>
</style>
