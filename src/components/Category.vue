<template>
  <!-- <div style="width: 80%;height:50%;overflow-y:scroll;padding-right: 15rem;box-sizing: content-box;"> -->
  <div class="h-50" style="overflow-y:scroll;">
    <b-row class="justify-content-md-center">
      <b-list-group class="h-50">
        <b-list-group-item
          v-for="category in categories"
          :key="category.id"
          @click="selectCategory(category)"
          >{{ category.name }}</b-list-group-item
        >
      </b-list-group>
    </b-row>
  </div>
</template>

<script>
export default {
  name: "Category",
  data: () => ({
    categories: null
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
          this.categories = jsonData.trivia_categories;
        });
      return categoryList;
    }
  }
};
</script>

<style></style>
