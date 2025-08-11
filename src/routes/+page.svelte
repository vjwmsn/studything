<svelte:options runes/>

<script>
    //imports
    import arrowfoward from "$lib/assets/foward-arrow.svg"
</script>


<div class="body">

<div id="topbar" class="bar topbar">
    <div id="left-side">
        <button id="leave-button" class="regular-button">Leave</button>
    </div>
    <div id="quiz-name" class="text-box">
        <span class="align-center">Spanish Glossary Week 34</span>
    </div>
    <div id="question-count" class="text-box">
        <span class="align-center">15 / 20 Questions Remaining</span>
    </div>
    <div id="right-side">
        <button id="next-question" class="regular-button">Skip Question</button>
    </div>
</div>

<div id="footer" class="footer">
    <div class="bar"></div>

</div>



</div>
<style>

    #topbar {
        position: relative;
        display: flex;
        align-items: center;
        justify-content: flex-start;
        padding-left: 5px;
        padding-right: 5px;
    }

    #left-side {
        display: flex;
        flex-direction: row;
        align-items: center;
        height: 100%;
    }

    #right-side {
        display: flex;
        flex-direction: row;
        align-items: center;
        height: 100%;
    }


    .body {
        background-color: hsl(0, 0%, 90%);
        display: flex;
        flex-direction: column;
        min-height: 100vh;
        min-width: 100%;
    }

    .topbar {

    }

    .bar {
        display: flex;
        flex-direction: row;
        align-items: center;
        min-height: 3rem;
        max-height: 3rem;
        background: linear-gradient(hsl(0, 0%, 100%), hsl(0,0%,85%));
        padding: 10px;
    }

    .footer {
        bottom: 0;
        position: absolute;
        width: 100%;
    }

    #leave-button {
        order: 1;
        margin-bottom: auto;
        margin-top: auto;
        margin-left: 10px;
    }

    #question-count {
        flex: 1;
        margin-bottom: auto;
        margin-top: auto;
        margin-left: 10px;
    }

    #quiz-name {
        margin-right: auto;
        z-index: 1;
        
    }

    #next-question {
        order: 2;
        margin-bottom: auto;
        margin-top: auto;
        margin-right: 10px;
    }

    .regular-button {
        border: 0;
        border-radius: 10px;
        background: linear-gradient(hsl(257, 90%, 50%),hsl(257, 90%, 35%));
        padding: 10px;
        color: hsl(0, 0%, 85%);
        opacity: 100%;
        transition: 0.3s;
        filter: drop-shadow(0 0 0 1.5rem hsl(257, 90%, 50%));
        font-weight: 800;
        font-family: "Mozilla Text", "sans-serif";
        margin-left: 5px;
        margin-right: 5px;
        text-align: center;
        display: flex;           
        align-items: center;     
    }

    .regular-button:hover {filter: drop-shadow(0 0 0.6rem hsl(257, 100%, 50%));}

    .text-box {
        border: 0;
        border-radius: 10px;
        background: linear-gradient(hsla(0, 0%, 50%, 0.2), hsla(0,0%,50%, 0.1));
        padding: 10px;
        color: hsl(0, 0%, 25%);
        font-weight: 800;
        align-items: center;
        display: flex;
        margin-left: 5px;
        margin-right: 5px;

    }

    .align-center {
        margin: auto;
        margin-bottom: auto;
        margin-top: auto;
    }

    .align-right {
        margin-left: auto;
        margin-bottom: auto;
        margin-top: auto;
    }

    .align-left {
        margin-right: auto;
        margin-bottom: auto;
        margin-top: auto;
    }
</style>