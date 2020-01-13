<template>
  <div>
    <b-navbar toggleable="lg" type="light" variant="light">
      <b-navbar-brand href="#">
        <router-link to="/">Beb-La</router-link>
      </b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
          <b-nav-item href="#">
            <router-link to="/">Home</router-link>
          </b-nav-item>
          <b-nav-item href="#">
            <router-link to="/about">About</router-link>
          </b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-item-dropdown text="Categories" right>
            <b-dropdown-item
              href="#"
              v-for="(category, index) in categories"
              :key="category.id"
              @click="selectCategory(category)"
              >{{ category.name }} / Questions in category ({{
                sortNumberOfQuestions(index)
              }})</b-dropdown-item
            >
          </b-nav-item-dropdown>

          <!-- <b-nav-item-dropdown right> -->
          <!-- Using 'button-content' slot -->
          <!-- <template v-slot:button-content>
              User
            </template>
            <b-dropdown-item href="#">Profile</b-dropdown-item>
            <b-dropdown-item href="#">Sign Out</b-dropdown-item>
          </b-nav-item-dropdown> -->
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "NavBar",
  data: () => ({
    categories: null,
    questionNumber: {}
  }),
  mounted: function() {
    this.getCategories();
    this.getNumberOfQuestions();
  },
  methods: {
    selectCategory(category) {
      this.$emit("selected", category);
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
    },
    async getNumberOfQuestions() {
      const questionList = await fetch(
        "https://opentdb.com/api_count_global.php",
        {
          method: "get"
        }
      )
        .then(response => {
          return response.json();
        })
        .then(jsonData => {
          this.questionNumber = jsonData.categories;
        });
      return questionList;
    },
    sortNumberOfQuestions(x) {
      const questionArray = [];
      for (let prop in this.questionNumber) {
        if (this.questionNumber.hasOwnProperty(prop)) {
          questionArray.push(this.questionNumber[prop]);
        }
      }
      for (let i = 0; i < questionArray.length; i++) {
        if (i === x) {
          return questionArray[i].total_num_of_questions;
        }
      }
    }
  }
};
</script>

<style></style>
