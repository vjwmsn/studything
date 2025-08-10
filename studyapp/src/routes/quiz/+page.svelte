<script>
    import Bar from "$lib/Bar.svelte"
    import Btn from "$lib/TextButton.svelte"
    import Label from "$lib/TextLabel.svelte"
    import ProgressBar from "$lib/ProgressBar.svelte";

    let submitButtonStates = ["Skip Question", "Submit", "Next Question"]
    let submitButtonState = 0
    

    let questionCount = $state(15)
    let questionsCompleted = $state(0)
    let percentageCompleted = $state(0)

    let count = $state(50)

    function submit () {
        questionsCompleted++
        percentageCompleted = calculatePercentage(questionCount, questionsCompleted)
        console.log(percentageCompleted)
    }

    function calculatePercentage (total, completed) {
        if (total === 0) return 0;
        return completed / total * 100;
    }
        
</script>

<div>
    <Bar>
        <Btn content="Leave"/>
        <Label content="Spanish Glossary Week 34"/>
        <ProgressBar content="{questionsCompleted}/{questionCount} Questions Completed - {Math.ceil(percentageCompleted)}%" align="fill-stretch" progress={percentageCompleted}/>
        <Btn content={submitButtonStates[submitButtonState]} align="right" onClick={submit}/>
    </Bar>
</div>
