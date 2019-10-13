<script>
  import Question from "./Question.svelte";

  export let quizName;

  let quiz = getQuiz();

  async function getQuiz() {
    const res = await fetch(
      "https://opentdb.com/api.php?amount=10&category=21&difficulty=medium&type=multiple"
    );
    const quiz = await res.json();
    return quiz;
  }

  function handleClick() {
    quiz = getQuiz();
  }
</script>

<h2>{quizName}</h2>
<div>
  <button on:click={handleClick}>Get Questions</button>
  {#await quiz}
    <p>Loading....</p>
  {:then data}
    {#each data.results as question}
      <Question {question} />
    {/each}
  {/await}
</div>
