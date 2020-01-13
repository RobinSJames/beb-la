<template>
  <div>
    <b-list-group>
      <b-list-group-item
        v-for="amount in amounts"
        :key="amount.id"
        @click="setAmount(amount.title)"
        >{{ amount.title }}</b-list-group-item
      >
    </b-list-group>
  </div>
</template>

<script>
export default {
  name: "Amount",
  data: () => ({
    amounts: [
      { id: 1, title: 10 },
      { id: 2, title: 20 },
      { id: 3, title: 30 },
      { id: 4, title: 40 },
      { id: 5, title: 50 }
    ]
  }),
  methods: {
    setAmount(x) {
      this.$emit("amount", x);
    }
  }
};
</script>

<style>
.list-group {
  margin-bottom: 15px;
}
.list-group-item:hover {
  background: #ddd;
  cursor: pointer;
}
</style>
