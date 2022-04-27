<script>
    import { fade, blur, fly, slide, scale } from 'svelte/transition';
    import { onMount, beforeUpdate, afterUpdate, onDestroy } from 'svelte';
    import Question from "./Question.svelte";
    let activeQuestion = 0;
    let score = 0;
    let quiz = getQuiz();

    onMount(() => {
        console.log("I mounted");
    });

    beforeUpdate(() => {
        console.log("Before Update");
    });

    afterUpdate(() => {
        console.log("After Update");
    });

    async function getQuiz() {
        const res = await fetch('https://opentdb.com/api.php?amount=10&category=21&type=multiple');
        const quiz = await res.json();
        console.log(quiz);
        return quiz;
    }
    
    function nextQuestion() {
        activeQuestion += 1;
    }
    
    function resetQuiz() {
        score = 0;
        activeQuestion = 0;
        quiz = getQuiz();
    }

    function addToScore() {
        score += 1;
    }

    // Reactive Statement
    $: if (score > 7) {
        alert("You won!");
        resetQuiz();
    }

    // Reactive Declaration
    $: questionNumber = activeQuestion + 1;
</script>

<style>
    .fade-wrapper {
        position: absolute;
    }
</style>

<div>
    <button on:click={resetQuiz}>Start New Quiz</button>

    <h3>My Score: {score}</h3>

    <h4>Question #{questionNumber}</h4>

    {#await quiz}
        Loading....
    {:then data} 
        {#each data.results as question, index}
            {#if index === activeQuestion}
            <div in:fly={{ x: 100 }} out:fly={{ x: -200 }} class="fade-wrapper">
                    <Question {addToScore} {nextQuestion} {question} />
                </div>
            {/if}
        {/each}
    {/await}


</div>
