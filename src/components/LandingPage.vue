<template>
  <div>
    <b-button pill @click="nextPage">SELECT GAME OPTIONS</b-button>
  </div>
</template>

<script>
export default {
  name: "LandingPage",
  methods: {
    nextPage() {
      this.$emit("clicked");
    }
  }
};
</script>

<style></style>
