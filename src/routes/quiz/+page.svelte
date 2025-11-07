<script>
    //import Topbar from "$lib/Bar.svelte"
    import Bar from "$lib/Bar.svelte"
    import Btn from "$lib/TextButton.svelte"
    import Label from "$lib/TextLabel.svelte"
    import ProgressBar from "$lib/ProgressBar.svelte";
    import InputField from "$lib/InputField.svelte";
    import { fade } from 'svelte/transition'
    import { slide } from 'svelte/transition'
    import ConvertingPoint from "$lib/ConvertingPoint.svelte";
    

    let submitButtonStates = ["Skip Question", "Submit Answer", "View Results", "Next Question","Try Again"]
    let submitButtonState = 0

    let commentTextPositive = ["Correct — Well done!", "Correct — Nice job!"]
    let commentTextNegative = ["Hmm, not quite right."]
    let commentText = $state("")
    
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

    let quesstionIsCorrect = $state(false)
    let limbo = $state(false)

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
                quesstionIsCorrect = true
                limboFunction("correct")
            } else {
                console.log("incorrect")
                limboFunction("incorrect")
            }
        } else {
             console.log("skipped")
             sliding = false
        }


        
    }

    function calculatePercentage (total, completed) {
        if (total === 0) return 0;
        return completed / total * 100;
    }


    function limboFunction (type) {
        if (type == "correct") {
        limbo = true
        inputIsDisabled = true
        commentText = commentTextPositive[Math.floor(Math.random() * commentTextPositive.length)]
        }

        if (type == "incorrect") {
            limbo = true
            inputIsDisabled = true
            commentText = commentTextNegative[Math.floor(Math.random() * commentTextNegative.length)]
            
        }

    }
    
    function limboFunctionPT2() {
        sliding = false
        limbo = false
        quesstionIsCorrect = false
        inputIsDisabled = false
    }

</script>

<title>{quizName} | StudyThing</title>

<div id="body">
    <Bar>
        <Btn content="Leave"/>
        <Label content={quizJSON.quizName}/>
        <ProgressBar content="{questionsCompleted}/{questionCount} Questions Completed - {Math.floor(percentageCompleted)}%" align="fill-stretch" progress={percentageCompleted}/>
        
        {#if inputValue !== "" & questionsCompleted !== questionCount & !limbo}
            <Btn content={submitButtonStates[1]} align="right" onClick={submit}/>
        {/if}
        {#if inputValue == "" & questionsCompleted !== questionCount}
            <Btn content={submitButtonStates[0]} align="right" onClick={submit}/>
        {/if}
        {#if questionsCompleted == questionCount}
            <Btn content={submitButtonStates[2]} align="right" onClick={submit}/>
        {/if}
        {#if limbo}
            <Btn content={submitButtonStates[3]} align="right" onClick={limboFunctionPT2}/>
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
                    <ConvertingPoint size=1.5rem active={quesstionIsCorrect}/>
                   <div style="display:flex; flex-direction:column; margin-left: 15px">
                    {#if !limbo}
                    <div style="display: flex; flex-direction:row; margin-bottom: 10px"> 
                    <span class="notouchy">Write "</span>
                    <span class="highlight-wavy">{quizJSON.quizWords[questionsCompleted].nativeWord}</span>
                    <span class="notouchy">" in {quizJSON.quizTargetLanguage}</span>
                    <span class="hidden notouchy" style="margin-left: 10px; color: hsl(0,0%,50%)">// correct!</span>
                    </div>
                    {/if}
                    {#if limbo}
                    <div style="display:flex; flex-direction:column; margin-left: 15px; margin-bottom: 10px;">
                    <span class="notouchy>" transition:fade>{commentText}</span>
                    </div>
                    {/if}

                <div style="display: flex; flex-direction: row; order: 2;">
                    
                    <InputField id="input" placeholder={inputPlaceholder} bind:value={inputValue} isDisabled={inputIsDisabled} onEnterUp={submit}/>
                    
                    <div style="margin-left: 5px; margin-top: 5px;">
                    {#if !limbo}
                    <Btn content="Submit" onClick={submit}/>
                    {/if}
                    {#if limbo}
                    <Btn content="Next Question" onClick={limboFunctionPT2}/>
                    {/if}
                    </div>
                    </div> 
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
