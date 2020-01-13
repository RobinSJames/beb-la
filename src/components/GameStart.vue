<template>
  <div>
    <b-button @click="createApiCall">START</b-button>
  </div>
</template>

<script>
export default {
  name: "GameStart",
  props: {
    amount: {
      type: Number,
      default: 0
    },
    category: {
      type: Object,
      default: () => ({})
    },
    difficulty: {
      type: String,
      default: ""
    },
    type: {
      type: String,
      default: ""
    }
  },
  data: () => ({
    apiCall: {}
  }),
  methods: {
    createApiCall() {
      this.apiCall.apiAmount = this.amount;
      this.apiCall.apiCategory = this.category;
      this.apiCall.apiDiffculty = this.difficulty;
      this.apiCall.apiType = this.type;
      this.$emit("api", this.apiCall);
    }
  }
};
</script>

<style></style>
