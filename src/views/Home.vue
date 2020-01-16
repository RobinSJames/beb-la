<template>
  <div class="home">
    <NavBar />
    <div v-if="token.response_code === 0" class="background">
      <LandingPage v-if="page === 1" @clicked="page++" class="landingpage" />
      <Amount v-if="page === 2" @amount="setAmount" class="amount" />
      <Category v-if="page === 3" @category="setCategory" class="category" />
      <Difficulty
        v-if="page === 4"
        @difficulty="setDifficulty"
        class="difficulty"
      />
      <GameStart
        v-if="page === 5"
        :amount="selectedAmount"
        :category="selectedCategory"
        :difficulty="selectedDifficulty"
        :type="type"
        @api="sendParams"
        class="gamestart"
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
.background {
  position: relative;
  background: rgba(255, 0, 0, 1);
  min-height: 100vh;
  width: 100%;
  overflow-x: hidden;
}
.landingpage,
.amount,
.category,
.difficulty,
.gamestart {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  overflow: hidden;
}
/* .category {
  position: absolute;
  top: 50%;
  left: 57%;
  transform: translate(-50%, -50%);
} */
</style>
