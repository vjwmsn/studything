<script>
    import Bar from "$lib/Bar.svelte"
    import Btn from "$lib/TextButton.svelte"
    import Label from "$lib/TextLabel.svelte"
    import ProgressBar from "$lib/ProgressBar.svelte";

    let {questionCount = 0, questionsCompleted = 0, percentageCompleted = 0, submitButtonState = 0, submitButtonStates = []} = $props()
</script>

    <Bar>
        <Btn content="Leave"/>
        <Label content={quizJSON.quizName}/>
        <ProgressBar content="{questionsCompleted}/{questionCount} Questions Completed - {Math.floor(percentageCompleted)}%" align="fill-stretch" progress={percentageCompleted}/>
        <Btn content={submitButtonStates[submitButtonState]} align="right" onClick={submit}/>
    </Bar>