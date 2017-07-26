<template>
  <div id="app">
    <div id="emitter">
      <div class="rings">
        <span v-for="n in 40" class="particle" v-bind:style="particleStyle(n)">
        </span>
      </div>
    </div>

    <!--<div v-for="(quiz, index) in quizez" v-show="index === questionindex">-->

    <!--  <h1>{{ quiz.category }}</h1>-->

    <!--  <h2>{{ quiz.question }}</h2>-->

    <!--  <ol>-->

    <!--    <li v-for="answer in quiz.incorrect_answers">-->
    <!--      <label>-->
    <!--        <input type="radio" name="answer" v-model="answers[index]" :value="answer"> {{answer}}-->
    <!--      </label>-->
    <!--    </li>-->
    <!--  </ol>-->
    <!--</div>-->
    <!--<div v-if="questionindex < quizez.length">-->
    <!--  <button v-if="questionindex > 0" v-on:click="prev">-->
    <!--  </button>-->
    <!--  <button v-on:click="next">-->

    <!--  </button>-->
    <!--</div>-->

    <!--<span v-if="questionindex == quizez.length">Your Total score is {{score}} / {{quizez.length}}</span>-->
  </div>
</template>

<script>
const quizQuestions = [
  {
    category: 'Entertainment: Film',
    type: 'multiple',
    difficulty: 'easy',
    question: 'Who directed "E.T. the Extra-Terrestrial" (1982)?',
    correct_answer: 'Steven Spielberg',
    incorrect_answers: [
      'Steven Spielberg',
      'Stanley Kubrick',
      'James Cameron',
      'Tim Burton',
    ],
  },
  {
    category: 'Entertainment: Video Games',
    type: 'multiple',
    difficulty: 'medium',
    question: 'What is the main character of Metal Gear Solid 2?',
    correct_answer: 'Raiden',
    incorrect_answers: [
      'Raiden',
      'Solidus Snake',
      'Big Boss',
      'Venom Snake',
    ],
  },
  {
    category: 'Science & Nature',
    type: 'multiple',
    difficulty: 'easy',
    question: 'What is the hottest planet in the Solar System?',
    correct_answer: 'Venus',
    incorrect_answers: [
      'Venus',
      'Mars',
      'Mercury',
      'Jupiter',
    ],
  },
  {
    category: 'Entertainment: Books',
    type: 'multiple',
    difficulty: 'hard',
    question: "What is Ron Weasley's middle name?",
    correct_answer: 'Bilius',
    incorrect_answers: [
      'Bilius',
      'Arthur',
      'John',
      'Dominic',
    ],
  },
  {
    category: 'Politics',
    type: 'multiple',
    difficulty: 'medium',
    question: 'Before 2011, "True Capitalist Radio" was known by a different name. What was that name?',
    correct_answer: 'True Conservative Radio',
    incorrect_answers: [
      'True Conservative Radio',
      'True Republican Radio',
      'Texan Capitalist Radio',
      'United Capitalists',
    ],
  },
  {
    category: 'Entertainment: Film',
    type: 'multiple',
    difficulty: 'medium',
    question: 'This movie contains the quote, "I love the smell of napalm in the morning!"',
    correct_answer: 'Apocalypse Now',
    incorrect_answers: [
      'Apocalypse Now',
      'Platoon',
      'The Deer Hunter',
      'Full Metal Jacket',
    ],
  },
  {
    category: 'History',
    type: 'multiple',
    difficulty: 'medium',
    question: 'The Herero genocide was perpetrated in Africa by which of the following colonial nations?',
    correct_answer: 'Germany',
    incorrect_answers: [
      'Germany',
      'Britain',
      'Belgium',
      'France',
    ],
  },
  {
    category: 'Entertainment: Music',
    type: 'boolean',
    difficulty: 'medium',
    question: 'Ashley Frangipane performs under the stage name Halsey.',
    correct_answer: 'True',
    incorrect_answers: [
      'True',
      'False',
    ],
  },
  {
    category: 'Entertainment: Books',
    type: 'multiple',
    difficulty: 'easy',
    question: 'Under what pseudonym did Stephen King publish five novels between 1977 and 1984?',
    correct_answer: 'Richard Bachman',
    incorrect_answers: [
      'Richard Bachman',
      'J. D. Robb',
      'Mark Twain',
      'Lewis Carroll',
    ],
  },
  {
    category: 'History',
    type: 'multiple',
    difficulty: 'medium',
    question: 'In what prison was Adolf Hitler held in 1924?',
    correct_answer: 'Landsberg Prison',
    incorrect_answers: [
      'Landsberg Prison',
      'Spandau Prison',
      'Ebrach Abbey',
      'Hohenasperg',
    ],
  },
];
export default {
  // name of the component
  name: 'app',
  // function that returns data to the components
  data() {
    return {
      // question index, used to show the current question
      questionindex: 0,
      // set the variable quizez to the questions defined earlier
      quizez: quizQuestions,
      // create an array of the length of the questions, and assign them to an empty value.
      answers: Array(quizQuestions.length).fill(''),
    };
  },
  // methods to be called in the component
  methods: {
    // Go to next question
    next() {
      this.questionindex += 1;
    },
    // Go to previous question
    prev() {
      this.questionindex -= 1;
    },
    random(m, n) {
      const mi = parseInt(m, 10);
      const ni = parseInt(n, 10);
      return Math.floor(Math.random() * ((ni - mi) + 1)) + mi;
    },
    particleStyle(n) {
      const r = () => Math.floor(256 * Math.random());
      const size = 25;
      return {
        width: `${size}px`,
        height: `${size}px`,
        animationDelay: `${n / 2}s`,
        backgroundColor: `rgba(${r()}, ${r()}, ${r()}, 0.5)`,
      };
    },
  },
  computed: {
    // calculate total score of the quiz person.
    score() {
      let total = 0;
      for (let i = 0; i < this.answers.length; i += 1) {
        if (this.answers[i] === this.quizez[i].correct_answer) {
          total += 1;
        }
      }
      return total;
    },
  },
};
</script>

<style lang="scss">
  $font-stack:    Helvetica, sans-serif;
  $primary-color: #333;
  body {
    font: 100% $font-stack;
    color: $primary-color;
    background-color: black;
    margin: 0px;
    
    #emitter {
      >.rings {
        >.particle {
          opacity:0;
          position: absolute;
          right: 0px;
          bottom: 0px;
          animation: rings 15s ease-in infinite;
          border-radius:100%;
        }
      }
    }
  }
  @keyframes rings {
    0% {
      opacity: 0;
    }
    20% {
      opacity: 1;
    }
    80% {
      opacity: 1;
    }
    100% {
      opacity: 0;
      transform:scale(200);
    }
  }
</style>