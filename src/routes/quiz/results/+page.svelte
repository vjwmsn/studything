<script>
    import Bar from "$lib/Bar.svelte"
    import Btn from "$lib/TextButton.svelte"
    import BreakdownBar from "$lib/BreakdownBar.svelte";
    import Table from "$lib/Table.svelte";
    import TableElement from "$lib/TableElement.svelte";

    let breakdownInfo = [
    { name: 'Correct', percentage: 30, bg: 'var(--color-accent-green)' },
    { name: 'Wrong', percentage: 30, bg: 'var(--color-accent-red)'},
    { name: 'Skipped', percentage: 40, bg: 'var(--color-accent-yellow)' }
    ]

    let answerResults = [
        {
            word: "Hablar",
            result: "Correct" },
        {
            word: "Comer",
            result: "Skipped"},
        {
            word: "Ordenador",
            result: "Incorrect"},
        {
            word: "Botella",
            result: "Correct"}
    ];

</script>

<svelte:head>
    <title>Results | StudyThing</title>
</svelte:head>

<Bar>
<span style="font-size: x-large; margin-left: 5px; font-weight: 600; color: var(--color-accent-90-50);">StudyThing</span>
<Btn content="Finish" align="right"/>
</Bar>

<h1 style="margin-left: auto; margin-right: auto; margin-top: 15vh;" class="header" >Nice work! Here are your results.</h1>
<div class="main">
<BreakdownBar zones={breakdownInfo} />
    <div class="row">
        <!--MEGA SPAGHETTI CODE-->

        {#if answerResults.length === 1}
            <Table>
                <TableElement self=true side=left text={answerResults[0].word}/>
            </Table>
            <Table>
                <TableElement self=true side=right text={answerResults[0].result}/>
            </Table>
        {/if}

        {#if answerResults.length === 2}
            <Table>
                <TableElement top=true side=left text={answerResults[0].word}/>
                <TableElement bottom=true side=left text={answerResults[1].word}/>
            </Table>
            <Table>
                <TableElement top=true side=right text={answerResults[0].result}/>
                <TableElement bottom=true side=right text={answerResults[1].result}/>
            </Table>
        {/if}

        {#if answerResults.length >= 3}
            <Table>
                <TableElement top=true side=left text={answerResults[0].word}/>
                {#each answerResults.slice(1, -1) as element, i (element.word + i)}
                    <TableElement middle=true side=left text={element.word}/>
                {/each}
                <TableElement bottom=true side=left text={answerResults[answerResults.length - 1].word}/>
            </Table>

            <Table>
                <TableElement top=true side=right text={answerResults[0].result}/>
                {#each answerResults.slice(1, -1) as element, i (element.result + i)}
                    <TableElement middle=true side=right text={element.result}/>
                {/each}
                <TableElement bottom=true side=right text={answerResults[answerResults.length - 1].result}/>
            </Table>
        {/if}


    </div>

</div>




<style>
    :global(body) {
        display: flex;
        flex-direction: column;
        height: 100vh;
        background: linear-gradient(hsl(0,0%,100%), hsl(0,0%,85%));
        
    }

    .row {
        display: flex;
        flex-direction: row;
        margin-top: 15px;
        overflow: scroll;
    }

    .header {

        font-size: xx-large;
        font-weight: 600;
    }

    .main {
        margin-top: 10px;
        margin-left: 25%;
        margin-right: 25%;
    }

    .table {
        height: auto;
        width: 50%;
        margin-top: 15px;
    }

    .table-element {
        background: linear-gradient(hsl(0, 0%, 100%), hsl(0, 0%, 98%));
        border: 1px solid;
        height: 2rem;
        border-color: hsl(0, 0%, 75%);
        display: flex;
        flex-direction: column;
        justify-content: center; 
        align-items: center;
        padding-left: 10px;
        padding-right: 10px;
        transition: all 0.5s
    }

    .table-element:hover {
        box-shadow: inset 0px 0px 5px hsl(0, 0%, 75%);
        filter: drop-shadow(0 0 0.05rem hsl(0, 0%, 24%));
    }

    .align-right {
        align-self: end;
        font-weight: 800;
    }

    .align-left {
        align-self: start;
    }

    .right {
        border-top-left-radius: 0px !important;
        border-bottom-left-radius: 0px !important;
    }

    .left {
        border-top-right-radius: 0px !important;
        border-bottom-right-radius: 0px !important;

    }

    .top{
        border-radius: 10px 10px 0px 0px;
        border-bottom: 0px none;
    }

    .middle {
        border-radius: 0px 0px 0px 0px;
        border-bottom: 0px none;
    }

    .end {
        border-radius: 0px 0px 10px 10px;
    }
/*
    .correct {
        background: linear-gradient(90deg, hsla(0 0% 100% / 0), var(--color-accent-green));
    }

    .skipped {
        background: linear-gradient(90deg, hsla(0 0% 100% / 0), var(--color-accent-yellow));
    }

    .incorrect {
        background: linear-gradient(90deg, hsla(0 0% 100% / 0), var(--color-accent-red));
    }
*/
</style>