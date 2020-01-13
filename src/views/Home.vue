<template>
  <div class="home">
    <NavBar />
    <div v-if="token.response_code === 0">
      <LandingPage />
      <Amount @amount="setAmount" />
      <Category @category="setCategory" />
      <Difficulty @difficulty="setDifficulty" />
      <GameStart
        :amount="selectedAmount"
        :category="selectedCategory"
        :difficulty="selectedDifficulty"
        :type="type"
        @api="log"
      />
      <GamePlay :api-object="apiObject" />
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
import GamePlay from "@/components/GamePlay";

export default {
  name: "home",
  components: {
    NavBar,
    LandingPage,
    Amount,
    Category,
    Difficulty,
    GameStart,
    GamePlay
  },
  data: () => ({
    token: null,
    type: "multiple",
    selectedAmount: null,
    selectedCategory: null,
    selectedDifficulty: null,
    apiObject: null
  }),
  mounted: function() {
    this.getToken();
  },
  methods: {
    log(x) {
      console.log(x);
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
    },
    setCategory(x) {
      this.selectedCategory = x;
    },
    setDifficulty(x) {
      this.selectedDifficulty = x;
    },
    setApiCall(x) {
      this.apiObject = x;
    }
  }
};
</script>
