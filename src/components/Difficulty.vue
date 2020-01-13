<template>
  <div>
    <b-list-group>
      <b-list-group-item
        v-for="difficulty in difficultyLevel"
        :key="difficulty.id"
        @click="setDifficulty(difficulty.title)"
        >{{ difficulty.title }}</b-list-group-item
      >
    </b-list-group>
  </div>
</template>

<script>
export default {
  name: "Difficulty",
  data: () => ({
    difficultyLevel: [
      { id: 1, title: "Easy" },
      { id: 2, title: "Medium" },
      { id: 3, title: "Hard" }
    ]
  }),
  methods: {
    setDifficulty(x) {
      this.$emit("difficulty", x);
    }
  }
};
</script>

<style></style>
