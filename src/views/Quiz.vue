<template>
  <div class="home">
    <v-row class="text-center">
      <v-col cols="12" class="pb-0">
        <v-img
          :src="require('../assets/printful-logo.png')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>
    </v-row>
    <v-row>
      <v-col
        cols="12"
        class="d-flex justify-center px-12 mb-12"
        style="font-size: 24px; min-height: 100px"
      >
        <span
          v-if="answersArr.length > 0 && answerIndex <= answersArr.length"
          class="d-flex justify-center"
          style="text-align: center"
        >
          {{ questionsArr[answerIndex].title }}</span
        >
        <span
          v-if="answerIndex > answersArr.length"
          class="d-flex justify-center"
          style="text-align: center"
        >
          Thank you {{ userName }} !
        </span>
      </v-col>
    </v-row>

    <template>
      <v-progress-linear
        color="#f2ca95"
        v-if="loadingQuestions"
        indeterminate
      ></v-progress-linear>
      <v-progress-linear
        v-else
        :color="progressColor"
        :value="progress"
        height="30"
        >{{ progress }}</v-progress-linear
      >
    </template>

    <v-row>
      <v-col cols="12" class="pb-0">
        <v-card flat>
          <v-tabs
            v-show="false"
            v-model="tab"
            background-color="transparent"
            grow
          >
            <v-tab v-for="item in items" :key="item"> </v-tab>
          </v-tabs>

          <v-tabs-items
            v-if="answerIndex <= answersArr.length"
            v-model="tab"
            class="pt-12"
          >
            <v-tab-item
              v-for="item in items"
              :key="item"
              transition="fade-transition"
              reverse-transition="fade-transition"
            >
              <v-card
                style="
                  background-color: white;
                  height: 55vh;
                  padding: 35px;
                  overflow-y: auto;
                "
                flat
              >
                <v-row>
                  <v-col
                    cols="12"
                    md="6"
                    v-for="(item, index) in answersArr"
                    :key="index"
                  >
                    <v-btn
                      dark
                      block
                      color="#03bbb6"
                      @click="chooseAnswer(item.id)"
                      style="min-height: 50px"
                      class="d-flex justify-center align-center"
                    >
                      <span v-show="!loadingAnswers"> {{ item.title }} </span>
                      <v-progress-circular
                        v-show="loadingAnswers"
                        indeterminate
                        color="#fff"
                      ></v-progress-circular>
                    </v-btn>
                  </v-col>
                </v-row>
              </v-card>
            </v-tab-item>
          </v-tabs-items>

          <v-row
            v-if="answersArr.length > 0 && answerIndex - 1 == answersArr.length"
            class="mt-12 pt-12"
          >
            <v-col cols="12" class="d-flex justify-center">
              TEST IS COMPLETED
            </v-col>
            <v-dialog
              v-model="dialog"
              fullscreen
              hide-overlay
              transition="dialog-bottom-transition"
              scrollable
            >
              <template v-slot:activator="{ on, attrs }">
                <v-row>
                  <v-col class="d-flex justify-center">
                    <v-btn
                      x-large
                      color="#ee4642"
                      dark
                      v-bind="attrs"
                      v-on="on"
                    >
                      get results
                    </v-btn>
                  </v-col>
                </v-row>
              </template>
              <v-card flat>
                <v-toolbar height="60px" dark color="#03bbb6">
                  <v-btn icon dark @click="home">
                    <v-icon>mdi-arrow-left</v-icon>
                  </v-btn>
                  <v-toolbar-title @click="home">Try again</v-toolbar-title>
                  <v-spacer></v-spacer>
                  <v-toolbar-items>
                    <v-btn dark text @click="dialog = false">
                      <v-icon>mdi-close</v-icon>
                    </v-btn>
                  </v-toolbar-items>
                </v-toolbar>
                <template>
                  <v-row style="min-height: 95vh">
                    <v-col class="d-flex justify-center align-end">
                      <span class="display-1 font-weight-bold mb-3">
                        {{ goodResults ? "Congratulations!" : "Keep trying!" }}
                      </span>
                    </v-col>
                    <v-col
                      cols="12"
                      class="d-flex justify-center align-start"
                      style="font-size: 28px"
                    >
                      You responded correctly
                      <strong class="px-2"> {{ results.correct }} </strong>
                      out of
                      <strong class="px-2"> {{ results.total }} </strong>
                    </v-col>
                    <v-col
                      cols="12"
                      class="d-flex justify-center align-end px-12"
                    >
                      <strong style="color: #ee4642; font-size: 24px">
                        Thank you for testing my quiz-app!
                      </strong>
                    </v-col>
                    <v-col
                      cols="12"
                      class="d-flex justify-center align-end px-12"
                    >
                      <span class="pl-3" style="font-size: 24px"
                        >If you wish to see more of my work on
                        <span
                          style="
                            color: #42b883;
                            font-weight: 600;
                            text-align: center;
                          "
                          >VUE.js</span
                        >
                        , you can remotely drive a mars rover by clicking the
                        button below:
                      </span>
                    </v-col>

                    <v-col
                      cols="12"
                      class="d-flex justify-center align-center"
                      style="background-color: #f2ca95"
                    >
                      <v-btn
                        dark
                        x-large
                        color="#ee4642"
                        to="https://constanza101.github.io/vue-leaflet-mars-rover/"
                      >
                        take me to mars!
                      </v-btn>
                    </v-col>
                  </v-row>
                </template>
              </v-card>
            </v-dialog>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import axios from "axios";

export default {
  name: "Quiz",
  components: {},
  data: () => {
    return {
      tab: 0,
      items: [],
      questionsArr: [],
      answersArr: [],
      answerIndex: 0,
      loadingAnswers: true,
      loadingQuestions: true,
      userAnswers: [],
      results: {},
      userName: "",
      dialog: false,
    };
  },
  computed: {
    questionId() {
      return this.questionsArr[this.tab].id;
    },
    progress() {
      let totalQuestions = this.questionsArr.length;
      let currentQuestion = this.answerIndex;
      let progress = null;
      currentQuestion < totalQuestions
        ? (progress = Math.ceil((currentQuestion / totalQuestions) * 100))
        : (progress = 100);

      return progress;
    },
    progressColor() {
      let color = "";
      let progress = this.progress;
      progress < 35
        ? (color = "#f2ca95")
        : progress > 35 && progress < 70
        ? (color = "#ee4642")
        : (color = "#03bbb6");
      return color;
    },
    goodResults() {
      let percentage = (this.results.total / 100) * this.results.correct;
      let isGoodResult = percentage > 70 ? true : false;
      return isGoodResult;
    },
  },
  async mounted() {
    this.userName = localStorage.getItem("userName", this.userName);
    await this.getQuestions();
    await this.getAnswers(this.questionId);
  },
  methods: {
    async chooseAnswer(answerId) {
      this.userAnswers[this.tab] = answerId;
      let isLastQuestion = this.tab + 1 == this.questionsArr.length;
      if (!isLastQuestion) {
        this.loadingAnswers = true;
        this.tab++;
        this.answerIndex++;
        await this.getAnswers(this.questionId);
      } else {
        this.tab++;
        this.answerIndex++;
        this.submitAnswers();
      }
    },
    home() {
      this.$router.push({
        name: "Home",
      });
    },

    //Axios:
    async getQuestions() {
      let quizId = this.$route.params.id;
      try {
        let response = await axios.get(
          `https://printful.com/test-quiz.php?action=questions&quizId=${quizId}`
        );
        let result = response.data;
        this.questionsArr = result;
        this.items = [];
        result.map((element, index) => this.items.push(index));
        this.loadingQuestions = false;
      } catch (err) {
        console.log(err);
        this.loadingQuestions = false;
      }
    },
    async getAnswers(questionId) {
      let quizId = this.$route.params.id;
      try {
        let response = await axios.get(
          `https://printful.com/test-quiz.php?action=answers&quizId=${quizId}&questionId=${questionId}`
        );
        let result = response.data;
        this.answersArr = result;
        this.loadingAnswers = false;
      } catch (err) {
        console.log(err);
        this.loadingAnswers = false;
      }
    },
    async submitAnswers() {
      let quizId = this.$route.params.id;
      let answersParams = "";
      this.userAnswers.map((id) => {
        answersParams += `&answers[]=${id}`;
      });

      try {
        let response = await axios.get(
          `https://printful.com/test-quiz.php?action=submit&quizId=${quizId}${answersParams}`
        );
        let result = response.data;
        this.results = result;
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
