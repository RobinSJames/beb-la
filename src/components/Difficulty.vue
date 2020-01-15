<template>
  <div>
    <b-list-group>
      <b-list-group-item
        v-for="difficulty in difficultyLevel"
        :key="difficulty.id"
        @click="setDifficulty(difficulty.value)"
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
      { id: 1, title: "Easy", value: "easy" },
      { id: 2, title: "Medium", value: "medium" },
      { id: 3, title: "Hard", value: "hard" }
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
