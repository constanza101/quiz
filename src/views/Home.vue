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
        <h1 class="display-2 font-weight-bold mb-3">Welcome to Quizful</h1>
      </v-col>
    </v-row>
    <v-form ref="form" v-model="valid">
      <v-row class="d-flex justify-center">
        <v-col class="d-flex justify-center" cols="10" md="4">
          <v-text-field
            label="Please enter your name here."
            placeholder="Eg. Constanza"
            filled
            :rules="[rules.textRequired]"
          ></v-text-field>
        </v-col>
      </v-row>

      <v-row class="d-flex justify-center">
        <v-col class="d-flex justify-center" cols="10" md="4">
          <v-select
            v-model="selectedQuiz"
            :items="quizes"
            item-text="title"
            item-value="id"
            filled
            label="Choose a quiz"
            :rules="[rules.idRequired]"
          ></v-select>
        </v-col>
      </v-row>
      <v-row class="d-flex justify-center pt-8">
        <v-btn v-on:click="submit" color="#03bbb6" dark depressed large>
          let's do the quiz!
        </v-btn>
      </v-row>
    </v-form>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import axios from "axios";

export default {
  name: "Home",
  components: {
    // HelloWorld
  },
  data: () => {
    return {
      selectedQuiz: null,
      quizes: [],
      valid: false,
      rules: {
        idRequired: (value) => !isNaN(parseFloat(value)) || "Requerido",
        textRequired: (value) => !!value || "Requerido",
      },
    };
  },
  async mounted() {
    await this.getQuizes();
  },
  methods: {
    submit(){
      if (this.$refs.form.validate()) {
        console.log("OK")
        this.$router.push({
        name: "Quiz",
        params: { id: this.selectedQuiz },
      });
      }
    },
    //Axios:
    async getQuizes() {
      try {
        let response = await axios.get(
          `https://printful.com/test-quiz.php?action=quizzes`
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
