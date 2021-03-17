<template>
  <div class="home">
    <v-row class="text-center">
      <v-col cols="12">
        <v-img
          :src="require('../assets/printful-logo.png')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3"> Quiz Title </h1>
      </v-col>
    </v-row>
   
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
// import axios from "axios";

export default {
  name: "Quiz",
  components: {
  },
  data: () => {
    return {

};
  },
  async mounted() {
    await this.getQuestions();
  },
  methods: {
    submit(){

    },
    //Axios:
    async getQuestions() {
      let quizID = this.$route.params.id
      console.log(quizID)
      try {
        let response = await axios.get(
          `https://printful.com/test-quiz.php?action=questions&quizId=${quizID}`
        );
        let result = response.data;
        console.log(result);
        this.quizes = result;
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
