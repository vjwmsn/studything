<script>
    //imports
    import arrowfoward from "$lib/assets/foward-arrow.svg"
</script>


<div class="body">


<div id="topbar" class="bar topbar">
    <button id="leave-button" class="regular-button">Leave</button>

    <div id="question-count" class="text-box align-left">
    <span class="align-center">15 / 20 Questions Remain</span>
    </div>

    <div id="quiz-name" class="text-box align-center">
    <span class="align-center">Spanish Glossary Week 34</span>
    </div>

    <button id="next-question" class="regular-button align-right">Skip Question
        <img src="arrowfoward" alt="arrow-foward">
    </button>

</div>

<div id="footer" class="footer">
    <div class="bar"></div>

</div>



</div>
<style>
    
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
        min-height: 3rem;
        max-height: 3rem;
        background: linear-gradient(hsl(0, 0%, 100%), hsl(0,0%,85%));
        flex: 1;
        padding: 10px;
    }

    .footer {
        bottom: 0;
        position: absolute;
        width: 100%;
    }

    #question-count {
        margin-left: 10px;
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

    }

    .align-center {
        margin: auto;
    }

    .align-right {
        margin-left: auto;
    }

    .align-left {
        margin-right: auto;
    }
</style>