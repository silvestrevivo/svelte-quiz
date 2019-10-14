<script>
  export let question;
  export let nextQuestion;
  export let addToScore;

  let isCorrect;
  let isAnswered = false;
  let answers = question.incorrect_answers.map(answer => {
    return {
      answer,
      correct: false
    };
  });

  let allAnswers = [
    ...answers,
    { answer: question.correct_answer, correct: true }
  ];

  shuffle(allAnswers);

  function shuffle(array) {
    array.sort(() => Math.random() - 0.5);
  }

  function checkQuestion(correct) {
    if (!isAnswered) {
      isAnswered = true;
      isCorrect = correct;
      if (isCorrect) {
        addToScore();
      }
    }
  }
</script>

<style>
  h5 {
    color: red;
  }
  .isCorrect {
    color: green;
  }
</style>

<h3>
  {@html question.question}
</h3>

{#if isAnswered}
  <h5 class:isCorrect>
    {#if isCorrect}You got it right{:else}Try it again{/if}
  </h5>
{/if}

{#each allAnswers as answer}
  <button on:click={() => checkQuestion(answer.correct)}>
    {@html answer.answer}
  </button>
{/each}

{#if isAnswered}
  <div>
    <button on:click={nextQuestion}>Next Question</button>
  </div>
{/if}
