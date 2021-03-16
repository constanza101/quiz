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
    <v-row class="d-flex justify-center">
      <v-col class="d-flex justify-center" cols="10" md="4">
        <v-text-field
          label="Please write down your name here."
          placeholder="Eg. Constanza"
          filled
        ></v-text-field>
      </v-col>
    </v-row>

    <v-row class="d-flex justify-center">
      <v-col class="d-flex justify-center" cols="10" md="4">
        <v-select  v-model="selectedQuiz" :items="quizes" item-text="title"
            item-value="id" filled label="Choose a quiz"   ></v-select>
      </v-col>
    </v-row>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: "Home",
  components: {
    // HelloWorld
  },
  data: () => {
    return {
      // quizes: Array,
      selectedQuiz: Number,
      quizes: [
        {
          id: 141,
          title: "Video Games",
        },
        {
          id: 169,
          title: "Numbers",
        },
        {
          id: 322,
          title: "Movies",
        },
      ],
    };
  },
  created() {
    this.getQuizes();
  },
  methods: {
   
    //Axios:
    async getQuizes() {
      try {
        let response = await axios.get(
          `/https://printful.com/test-quiz.php?action=quizzes`
        );
        let result = response.data;
        console.log(result)
        this.quizes = result;
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
