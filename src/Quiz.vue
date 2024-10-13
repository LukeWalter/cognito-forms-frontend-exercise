<script setup>
import { computed, ref, watch } from "vue";
import QuizAnswer from "./QuizAnswer.vue";

export default {
  props: {
    questions: {
      type: Array,
      required: true,
    },
  },
  components: {
    QuizAnswer: QuizAnswer,
  },
  data() {
    return {};
  },
  mounted() {
    console.log("This is working! :3");
  },
  setup(props) {
    const question = ref(0);
    const len = props.questions.length;

    const prev = () => {
      --question.value;
    };
    const next = () => {
      ++question.value;
    };

    const canPrev = computed(() => {
      return question.value > 0;
    });
    const canNext = computed(() => {
      return question.value < len - 1;
    });

    watch(question, (q) => {
      if (q < 0) {
        ++question.value;
      } else if (q >= len) {
        --question.value;
      }
    });

    return { question, prev, next, canPrev, canNext };
  },
};
</script>

<template>
  <!-- <pre>{{ JSON.stringify(questions, null, 2) }}</pre> -->
  <div>
    <button @click="prev" :disabled="!canPrev">Previous Question</button>
    <button @click="next" :disabled="!canNext">Next Question</button>
    <div>
      <h1>{{ questions[question].text }}</h1>
      <ul>
        <li v-for="a in questions[question].answers">
          <QuizAnswer :text="a" />
        </li>
      </ul>
    </div>
  </div>
</template>

<style>
@font-face {
  font-family: "Gilroy";
  src: url("~@/assets/fonts/<static_font_file>.ttf");
}
ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}
</style>
