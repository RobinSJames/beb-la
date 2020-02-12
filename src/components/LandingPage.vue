<template>
  <div>
    <AnimationPlay src="drink_shifting" class="animation" />
    <b-button pill @click="nextPage">SELECT GAME OPTIONS</b-button>
  </div>
</template>

<script>
import AnimationPlay from "./AnimationPlay";
export default {
  name: "LandingPage",
  components: { AnimationPlay },
  methods: {
    nextPage() {
      this.$emit("clicked");
    }
  }
};
</script>

<style>
.animation {
  height: 200px;
  width: 200px;
}
</style>
