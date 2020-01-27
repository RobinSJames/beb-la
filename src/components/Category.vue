<template>
  <!-- <div style="width: 80%;height:50%;overflow-y:scroll;padding-right: 15rem;box-sizing: content-box;"> -->
  <b-container fluid style="">
    <b-row
      v-for="categories in categoriesGroup"
      :key="categories.index"
      style=""
      class="justify-content-center"
    >
      <b-col
        v-for="category in categories"
        :key="category.id"
        @click="selectCategory(category)"
        cols="11"
        sm="3"
        style="background:white;margin:4px 4px;padding:10px 32px;"
        >{{ category.name }}</b-col
      >
    </b-row>
  </b-container>
</template>

<script>
import _ from "lodash";
export default {
  name: "Category",
  data: () => ({
    categoriesGroup: null
  }),
  mounted: function() {
    this.getCategories();
  },
  methods: {
    selectCategory(category) {
      this.$emit("category", category);
    },
    async getCategories() {
      const categoryList = await fetch("https://opentdb.com/api_category.php", {
        method: "get"
      })
        .then(response => {
          return response.json();
        })
        .then(jsonData => {
          this.categoriesGroup = _.chunk(jsonData.trivia_categories, 3);
        });
      return categoryList;
    }
  }
};
</script>

<style></style>
