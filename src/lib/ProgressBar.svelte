<script>
    let {content = "TextLabel", align = "", progress = 0} = $props();
</script>

<div class="progressBar {align}">
    <div class="progress_fill" style="width: {progress}%;"></div>
    <span class="progress_span notouchy" style="color: hsla(0, 0%, 0%, 0.75);">{content}</span>
</div>

<style>

    .progressBar {
        display: flex;
        align-items: center;
        border: 0px;
        border-radius: 10px;
        background: linear-gradient(hsl(0, 0%, 100%), hsl(0,0%,90%));
        filter: drop-shadow(0 0 0.05rem hsl(0, 0%, 24%));
        padding: 10px;
        color: hsl(0, 0%, 25%);
        margin-left: 5px;
        margin-right: 5px;
        text-align: center;
        font-family: "Mozilla Text", "sans-serif";
        font-weight: 800;
        height: 1.2rem;
        position: relative; /* Add this to create a positioning context */
    }

    .progress_fill {
        position: absolute;
        left: 0;
        height: 100%;
        background: linear-gradient(90deg, hsl(257, 90%, 50%),hsl(281, 100%, 50%),hsl(278, 100%, 65%));
        filter:  brightness(100%) drop-shadow(0 0 0.rem hsl(257, 90%, 50%));
        border-radius: 10px;
        transition: all 0.5s;
    }

    .fill-stretch {
        flex: 1;
        margin-left: 5px;
        margin-right: 10px;
    }

    .progress_span {
        position: absolute;
        left: 50%;
        top: 50%;
        transform: translate(-50%, -50%);

        
    }

    .notouchy {
        user-select: none;
    }

</style>