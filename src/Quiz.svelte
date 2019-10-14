<script>
  import { fade, blur, fly, slide, scale } from "svelte/transition";
  import Question from "./Question.svelte";

  let score = 0;
  let activeQuestion = 0;
  let quiz = getQuiz();

  async function getQuiz() {
    const res = await fetch(
      "https://opentdb.com/api.php?amount=10&category=21&difficulty=medium&type=multiple"
    );
    const quiz = await res.json();
    return quiz;
  }

  function nextQuestion() {
    activeQuestion = activeQuestion + 1;
  }

  function resetQuiz() {
    score = 0;
    quiz = getQuiz();
  }

  function addToScore() {
    score = score + 1;
  }
</script>

<style>
  .fade-wrapper {
    position: absolute;
  }
</style>

<div>
  <button on:click={resetQuiz}>Start a new Quiz!</button>

  <h3>My Score: {score}</h3>
  <h4>Question #{activeQuestion + 1}</h4>

  {#await quiz}
    <p>Loading....</p>
  {:then data}
    {#each data.results as question, index}
      {#if index === activeQuestion}
        <div transition:fade class="fade-wrapper">
          <Question {addToScore} {nextQuestion} {question} />
        </div>
      {/if}
    {/each}
  {/await}
</div>
