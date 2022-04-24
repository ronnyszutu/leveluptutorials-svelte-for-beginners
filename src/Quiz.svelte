<script>
    export let quizName = "Ronny Quiz";
    // let title = "";
    let a = 0;
    let b = 0;
</script>

<div>
    <h2>{quizName}</h2>
    
    <!-- <h4>{title}</h4>
    <input bind:value={title} type="text" /> -->

    <input type="number" bind:value={a}>
    <input type="number" bind:value={b}>
    <h4>{a + b}</h4>
</div>