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
        style="font-size: 24px; min-height: 100px;"
      >
      <span v-if="answersArr.length > 0"  class="d-flex justify-center" style="text-align: center">  {{ questionsArr[tab].title }}</span>
       
      </v-col>
    </v-row>

    <template>
      <v-progress-linear color="#03bbb6" v-if="loadingQuestions" indeterminate></v-progress-linear>
      <v-progress-linear :color="progressColor" v-else :value="progress"></v-progress-linear>
    </template>

    <v-row>
      <v-col cols="12" class="pb-0">
        <v-card flat>
          <v-tabs v-show="false" v-model="tab" background-color="transparent" grow>
            <v-tab v-for="item in items" :key="item"> </v-tab>
          </v-tabs>

          <v-tabs-items v-model="tab" class="pt-12">

            <v-tab-item  v-for="item in items" :key="item"  transition="fade-transition" reverse-transition="fade-transition">
              <v-card style="background-color: white; height: 55vh; padding: 35px; overflow-Y: auto" flat>
                <v-row>
                  <v-col
                    cols="12"
                    md="6"
                    v-for="(item, index) in answersArr"
                    :key="index"
                  >
                    <v-btn dark block color="#03bbb6" @click="chooseAnswer" style="min-height: 50px;" class="d-flex justify-center align-center">
                      <span v-show="!loadingAnswers"> {{ item.title }} </span> 
                      <v-progress-circular v-show="loadingAnswers" indeterminate  color="#fff"></v-progress-circular>
                    </v-btn>
                  </v-col>
                </v-row>
              </v-card>
            </v-tab-item>
          </v-tabs-items>
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
      loadingAnswers: true,
      loadingQuestions: true
    };
  },
  computed: {
    questionId() {
      return this.questionsArr[this.tab].id;
    },
    progress() {
      let totalQuestions = this.questionsArr.length;
      let currentQuestion = this.tab + 1;
      let progress = Math.ceil((currentQuestion / totalQuestions) * 100);
      console.log(progress);
      return progress;
    },
    progressColor(){
      let color = ""
      let progress = this.progress
      progress < 35 ? color = '#f2ca95' : progress > 35 &&  progress  < 70 ? color = '#ee4642' :  color = '#03bbb6';
      return color;
    }

  },
  async mounted() {
    await this.getQuestions();
    await this.getAnswers(this.questionId);
  },
  methods: {
    submit() {},
    
    async chooseAnswer(){
      this.loadingAnswers = true
      this.tab++
      // this.answersArr = []
      await this.getAnswers(this.questionId)
      // this.tab++
    },
    //Axios:
    async getQuestions() {
      let quizID = this.$route.params.id;
      console.log(quizID);
      try {
        let response = await axios.get(
          `https://printful.com/test-quiz.php?action=questions&quizId=${quizID}`
        );
        let result = response.data;
        console.log(result);
        this.questionsArr = result;
        this.items = [];
        result.map((element, index) => this.items.push(index));
        this.loadingQuestions = false
      } catch (err) {
        console.log(err);
        this.loadingQuestions = false
      }
    },
    async getAnswers(questionId) {
      console.log("questionId");
      console.log(questionId);
      let quizID = this.$route.params.id;
      console.log(quizID);
      try {
        let response = await axios.get(
          `https://printful.com/test-quiz.php?action=answers&quizId=${quizID}&questionId=${questionId}`
        );
        let result = response.data;
        console.log(result);
        this.answersArr = result;
        this.loadingAnswers = false
      } catch (err) {
        console.log(err);
        this.loadingAnswers = false
      }
    },
  },
  watch: {
    tab: function (val) {
      console.log(val);
      // let questionId = this.questionsArr[val].id
      // this.getAnswers(questionId)
    },
  },
};
</script>
