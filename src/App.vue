<template>
  <div class="ctr">
    <transition name="fade" mode="out-in">
      <questions
        v-if="questionsAnswered < questions.length"
        :questions="questions"
        :questionsAnswered="questionsAnswered"
        @question-answered="questionAnswered"
      />
      <result v-else :results="results" :totalCorrect="totalCorrect" />
    </transition>

    <button
      type="button"
      class="reset-btn"
      @click.prevent="reset"
      v-if="questionsAnswered === questions.length"
    >
      Refaire
    </button>
  </div>
</template>

<script>
import Questions from './components/Questions.vue';
import Result from './components/Result.vue';

export default {
  name: 'App',
  components: {
    Questions,
    Result,
  },
  data() {
    return {
      questionsAnswered: 0,
      totalCorrect: 0,
      questions: [
        {
          q: 'Le résultat de 6 * 7 + 8 = ?',
          answers: [
            {
              text: '49',
              is_correct: false,
            },
            {
              text: '50',
              is_correct: true,
            },
            {
              text: '51',
              is_correct: false,
            },
            {
              text: '52',
              is_correct: false,
            },
          ],
        },
        {
          q: "Trouver l'intrus :",
          answers: [
            {
              text: 'Fève',
              is_correct: false,
            },
            {
              text: 'Topinambour',
              is_correct: false,
            },
            {
              text: 'Litchi',
              is_correct: true,
            },
            {
              text: 'Pomme de terre',
              is_correct: false,
            },
          ],
        },
        {
          q: 'Trouver la lettre manquante Ca*sse :',
          answers: [
            {
              text: 'e',
              is_correct: false,
            },
            {
              text: 'i',
              is_correct: true,
            },
            {
              text: 'u',
              is_correct: false,
            },
          ],
        },
      ],
      results: [
        {
          min: 0,
          max: 2,
          title: 'Refaire à noveau !',
          desc: "Faire un p'tit effort et vous reussirez !",
        },
        {
          min: 3,
          max: 3,
          title: 'Toutes les réponses apportées sont justes !',
          desc: 'Excellent !',
        },
      ],
    };
  },
  methods: {
    questionAnswered(is_correct) {
      if (is_correct) {
        this.totalCorrect++;
      }

      this.questionsAnswered++;
    },
    reset() {
      this.questionsAnswered = 0;
      this.totalCorrect = 0;
    },
  },
};
</script>
