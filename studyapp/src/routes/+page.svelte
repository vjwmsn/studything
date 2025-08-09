<script>
    let count =  $state(0)
</script>

<div class="topbar">
    <button class="regular-button">Leave</button>
</div>

<style>
    
    

    .topbar {
        display: flex;
        flex-direction: row;
        min-height: 3rem;
        background-color: hsl(0, 0%, 90%);
        flex: 1;
        padding: 10px;
    }

    .regular-button {
        border: 0;
        border-radius: 10px;
        background-color: hsl(0, 100%, 55%);
        padding: 10px;
        color: white;
        opacity: 100%;
        transition: 0.3s;
    }

    .regular-button:hover {opacity: 60%;}

</style>