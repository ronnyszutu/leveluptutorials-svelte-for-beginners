<script>
	import Quiz from "./Quiz.svelte";
</script>

<style>
	:global(body) {
		background: #524763;
	}

	h1 {
		color: white;
		text-align: center;
	}

	main {
		background: white;
		border-radius: 15px;
		padding: 40px;
	}
</style>

<h1>Level Up Quiz</h1>

<main>
	<Quiz />
</main>