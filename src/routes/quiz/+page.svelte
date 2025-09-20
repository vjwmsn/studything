<script>
    //import Topbar from "$lib/Bar.svelte"
    import Bar from "$lib/Bar.svelte"
    import Btn from "$lib/TextButton.svelte"
    import Label from "$lib/TextLabel.svelte"
    import ProgressBar from "$lib/ProgressBar.svelte";
    import InputField from "$lib/InputField.svelte";
    import { fade } from 'svelte/transition'

    let submitButtonStates = ["Skip Question", "Submit Answer", "View Results"]
    let submitButtonState = 0
    
    let quizJSON = {
        "quizName": "Untitled Quiz",
        "testMode": true, // basically you don't know your results until the end of the quiz with test mode
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
            {"nativeWord": "Ice Cream", "targetWord": "Helado"},
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

    let sliding = $state(true)

    function handleOutroEnd() {
        questionsCompleted++;
        inputValue = "";
        percentageCompleted = calculatePercentage(questionCount, questionsCompleted);
        sliding = true; 
    }

    function submit() {
        if (!sliding) return;

        const currentTarget = wordArray[questionsCompleted].targetWord.trim().toLowerCase();
        const userInput = inputValue.trim().toLowerCase();

        if (userInput !== "") {
            if (userInput === currentTarget) {
                console.log("correct")
            } else {
                console.log("incorrect")
            }
        } else {
             console.log("skipped")
        }


        sliding = false;
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
        
        {#if inputValue !== "" & questionsCompleted !== questionCount}
            <Btn content={submitButtonStates[1]} align="right" onClick={submit}/>
        {/if}
        {#if inputValue == "" & questionsCompleted !== questionCount}
            <Btn content={submitButtonStates[0]} align="right" onClick={submit}/>
        {/if}
        {#if questionsCompleted == questionCount}
            <Btn content={submitButtonStates[2]} align="right" onClick={submit}/>
        {/if}

    </Bar>

    <div class="main">
        {#if sliding & questionsCompleted !== questionCount}
            <div
                id="main-pt2"
                class="question-header"
                transition:fade={{ duration: 300 }}
                onoutroend={handleOutroEnd}>
                <div style="display: flex; flex-direction: row; margin-bottom: 10px;">
                    <span class="notouchy">Write "</span>
                    <span class="highlight-wavy">{quizJSON.quizWords[questionsCompleted].nativeWord}</span>
                    <span class="notouchy">" in {quizJSON.quizTargetLanguage}</span>
                    <span class="hidden notouchy" style="margin-left: 10px; color: hsl(0,0%,50%)">// correct!</span>
                </div>
                <div style="display: flex; flex-direction: row;">
                    
                    <InputField id="input" placeholder={inputPlaceholder} bind:value={inputValue} isDisabled={inputIsDisabled} onEnterUp={submit}/>
                    
                    <div style="margin-left: 5px; margin-top: 5px;">
                    <Btn content="Submit" onClick={submit}/>
                    </div>
                </div>
            </div>
        {/if}
        {#if questionsCompleted == questionCount}
        <div class="question-header"
        transition:fade={{ duration: 400 }}
        onoutroend={handleOutroEnd}
        style="display: flex; flex-direction: column;">
            <span style="margin: 10px;">Quiz Complete. Well done!</span>
            <Btn content="View Results"/>
        </div>
        {/if}
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
        margin-top: 8%;
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
        animation-duration: 0.5s;
    }

    .slide-out {
        animation-name: slide-out;
        animation-duration: 0.5s;
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
        to {
            translate: 50vw 0;
            opacity: 0%;
        }
        
    }

    .highlight-wavy {
        text-decoration: var(--color-accent-1) wavy underline;
        font-weight: 900;
    }

    .notouchy {
        user-select: none;
    }
 </style>
