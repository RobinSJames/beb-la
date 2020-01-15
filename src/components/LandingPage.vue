<template>
  <div>
    <p>Click on the button to start the game</p>
    <b-button @click="nextPage">START</b-button>
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
