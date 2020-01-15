<template>
  <div class="home">
    <NavBar />
    <div v-if="token.response_code === 0" class="background">
      <LandingPage v-if="page === 1" @clicked="page++" />
      <Amount v-if="page === 2" @amount="setAmount" />
      <Category v-if="page === 3" @category="setCategory" />
      <Difficulty v-if="page === 4" @difficulty="setDifficulty" />
      <GameStart
        v-if="page === 5"
        :amount="selectedAmount"
        :category="selectedCategory"
        :difficulty="selectedDifficulty"
        :type="type"
        @api="sendParams"
      />
    </div>
  </div>
</template>

<script>
import NavBar from "@/components/NavBar";
import LandingPage from "@/components/LandingPage";
import Amount from "@/components/Amount";
import Category from "@/components/Category";
import Difficulty from "@/components/Difficulty";
import GameStart from "@/components/GameStart";

export default {
  name: "home",
  components: {
    NavBar,
    LandingPage,
    Amount,
    Category,
    Difficulty,
    GameStart
  },
  data: () => ({
    token: null,
    type: "multiple",
    selectedAmount: null,
    selectedCategory: null,
    selectedDifficulty: null,
    apiObject: null,
    page: 1
  }),
  created: function() {
    this.getToken();
  },
  methods: {
    sendParams(x) {
      this.$router.push({
        name: "about",
        params: x
      });
    },
    async getToken() {
      const token = await fetch(
        "https://opentdb.com/api_token.php?command=request",
        {
          method: "get"
        }
      )
        .then(response => {
          return response.json();
        })
        .then(jsonData => {
          this.token = jsonData;
        });
      return token;
    },
    setAmount(x) {
      this.selectedAmount = x;
      this.page++;
    },
    setCategory(x) {
      this.selectedCategory = x;
      this.page++;
    },
    setDifficulty(x) {
      this.selectedDifficulty = x;
      this.page++;
    }
  }
};
</script>

<style scoped>
/* .background {
  background: rgba(255, 0, 0, 1);
} */
</style>
