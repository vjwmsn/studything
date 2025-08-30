<script>
    //import Topbar from "$lib/Bar.svelte"
    import Bar from "$lib/Bar.svelte"
    import Btn from "$lib/TextButton.svelte"
    import Label from "$lib/TextLabel.svelte"
    import ProgressBar from "$lib/ProgressBar.svelte";
    import InputField from "$lib/InputField.svelte";

    let submitButtonStates = ["Skip Question", "Submit", "Next Question"]
    let submitButtonState = 0
    
    let quizJSON = {
        "quizName": "Untitled Quiz",
        "quizNativeLanguage": "English",
        "quizTargetLanguage": "Spanish",
        "forcePerfectDiacritic": false, // forces the user to spell perfect diacritic marks e.g "é" would be marked correct and "e" wouldn't.
        "forcePerfectPunctuation": false, // forces the user to spell with perfect punctuation e.g "Hello world!" would be marked correct and "Hello world" wouldn't.
        "forcePerfectLetterCases": false, // forces the user to spell with perfect letter cases e.g "E" would be marked correct and "e" wouldn't.
        "quizWords": [
            {"nativeWord": "To speak", "targetWord": "Hablar"},
            {"nativeWord": "To eat", "targetWord": "Comer"},
            {"nativeWord": "Computer", "targetWord": "Ordenador"},
            {"nativeWord": "Bottle", "targetWord": "Bottella"},
            {"nativeWord": "", "targetWord": ""}, // NO TOUCHY
        ]
    }

    let wordArray = quizJSON.quizWords
    let quizName = quizJSON.quizName

    let questionCount = $state(quizJSON.quizWords.length - 1) // i know this is a bandage fix but whatever, who cares?
    let questionsCompleted = $state(0)
    let percentageCompleted = $state(0)

    let inputValue = $state("")
    let inputPlaceholder = $state("Type your answer here")
    let inputIsDisabled = $state(false)

    function submit () {

        console.log(percentageCompleted)

        console.log(wordArray[questionsCompleted].targetWord)
        console.log(inputValue)


        if (inputValue !== "") {
            if (wordArray[questionsCompleted].targetWord == inputValue) {
                questionsCompleted++
                console.log("correct!")
            } else {
                console.log("incorrect!")
            }
        } else {
            questionsCompleted++
            mainHolder.classList.remove("fade in")
        }

        inputValue = ""
        percentageCompleted = calculatePercentage(questionCount, questionsCompleted)

    }

    function calculatePercentage (total, completed) {
        if (total === 0) return 0;
        return completed / total * 100;
    }

        
</script>

<title>StudyThing - {quizName}</title>

<div id="body">
    <Bar>
        <Btn content="Leave"/>
        <Label content={quizJSON.quizName}/>
        <ProgressBar content="{questionsCompleted}/{questionCount} Questions Completed - {Math.floor(percentageCompleted)}%" align="fill-stretch" progress={percentageCompleted}/>
        <Btn content={submitButtonStates[submitButtonState]} align="right" onClick={submit}/>
    </Bar>

    <div class="main">
        <div id="main-pt2" class="question-header slide-in">

            <div style="display: flex; flex-direction: row;">
                <span class="notouchy">Write "</span>
                <span class="highlight-wavy notouchy">{quizJSON.quizWords[questionsCompleted].nativeWord}</span>
                <span class="notouchy">" in {quizJSON.quizTargetLanguage}</span>
                <span class="hidden notouchy" style="margin-left: 10px; color: hsl(0,0%,50%)">// correct!</span>
        </div>

            <div style="display: flex; flex-direction: row; max-width: 100%;">
                    <InputField id="input" placeholder={inputPlaceholder} bind:value={inputValue} isDisabled={inputIsDisabled}/>
                
            </div>

        </div>
       
    </div>

</div>

 <style>

    .hidden {
        display: none;
    }



    #body {
        display: flex;
        flex-direction: column;
        height: 100vh;
        background: linear-gradient(hsl(0,0%,100%), hsl(0,0%,85%));
        
    }

    .main {
        display: flex;
        align-items: center;
        justify-content: center;
        min-height: 50px;
        flex: 1;
        margin-left: 10%;
        margin-right: 10%;
        margin-top: 5%;
        border-radius: 10px;
    }

    .question-header {
        margin-bottom: 40%;
        font-size: xx-large;
        font-weight: 600;
        color: hsl(0,0%,25%);
    }

    .slide-in {
        animation-name: slide-in;
        animation-duration: 1s;
    }

    @keyframes slide-in {
        from {
            translate: 50vw 0;
            opacity: 0%;
        }

        to {
            translate: 0 0;
            opacity: 100%;
        }
    }

    @keyframes slide-out {
        from {
            translate: 0 0;
            opacity: 100%;
        }
        
    }

    .highlight-wavy {
        text-decoration: hsl(257, 90%, 50%) wavy underline;
        font-weight: 900;
    }

    .notouchy {
        user-select: none;
    }
 </style>
