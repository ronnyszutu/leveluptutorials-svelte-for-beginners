<script>
    let result;
    let correctAnswer = "b";
    let answers = ["a", "b", "c", "d"];
    let quiz = getQuiz();

    function pickAnswer(answer){
        if (answer === correctAnswer) {
            return (result = "Correct!");
        }
        result = "OOPS";
    }

    async function getQuiz() {
        const res = await fetch('https://opentdb.com/api.php?amount=10&category=21&type=multiple');
        const quiz = await res.json();
        console.log(quiz);
        debugger;
    }
</script>

<style>
    h4 {
        /* color: red; */
    }
</style>

<div>
    <button on:click={getQuiz}>Get New Questions</button>
    {#if result}
        <h4>{result}</h4>
    {:else}
        <h5>Please pick an answer</h5>
    {/if}

    <h3>{quiz.results[0].question}</h3>

    {#each answers as answer}
        <button on:click={() => pickAnswer(answer)}>
            Answer {answer.toUpperCase()}
        </button>
    {/each}
</div>
