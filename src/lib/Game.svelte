<script>
    let tics = {
        aA: '',
        aB: '',
        aC: '',
        bA: '',
        bB: '',
        bC: '',
        cA: '',
        cB: '',
        cC: '',
    };
    let player = 'X';
    let gameOver = '';
    let message = `It is ${player}'s turn.`;
    const reset = () => {
      tics = {
        aA: '',
        aB: '',
        aC: '',
        bA: '',
        bB: '',
        bC: '',
        cA: '',
        cB: '',
        cC: '',
    };
    player = "X";
    gameOver = "";
    message = `It is ${player}'s turn.`;
    }
    const checkStatus = () =>{
        const checkAllEmpties = Object.entries(tics).flatMap((entry) => entry[1]).filter(entry => entry === '').length;
        if(checkAllEmpties === 0) gameOver = "No Winner";

        if(tics.aA && tics.aA === tics.aB && tics.aA === tics.aC) gameOver = player ;
        if(tics.bA && tics.bA === tics.bB && tics.bA === tics.bC) gameOver = player ;
        if(tics.cA && tics.cA === tics.cB && tics.cA === tics.cC) gameOver = player ;
        if(tics.aA && tics.aA === tics.bA && tics.aA === tics.cA) gameOver = player ;
        if(tics.aB && tics.aB === tics.bB && tics.aB === tics.cB) gameOver = player ;
        if(tics.aC && tics.aC === tics.bC && tics.aC === tics.cC) gameOver = player ;
        if(tics.aA && tics.aA === tics.bB && tics.aA === tics.cC) gameOver = player ;
        if(tics.cA && tics.cA === tics.bB && tics.cA === tics.aC) gameOver = player ;
    };

    function handleMessage(){
        if(gameOver === 'No Winner'){ message = `No more plays left and no winner!`; return}
        if(gameOver === 'X' || gameOver === 'O'){ message = `The winner is ${player}`; return}
        message = `It is ${player}'s turn.`
    }

    const handleClick = (key) =>{
        if(gameOver !== '') return
        if(tics[key] !== '') return
        tics[key] = player;
        checkStatus();
        handleMessage();
        if(gameOver !== '') return
        player = player === 'X'? "O" : "X";

    }

  </script>


<h2>{message}</h2>
{#if gameOver !== ''}
<button  on:click={() =>reset()}>Reset?</button>
{/if}


<div class="tiles-container">
    {#each Object.entries(tics) as item}
    <div class="tiles" on:keydown={()=>handleClick(item[0])} on:click={()=>handleClick(item[0])}>{item[1]}</div>
    {/each}
    

    
</div>

<style>
    .tiles-container {
        display: grid;
        grid-template-columns: auto auto auto;
        padding: 2em;
        margin: 2em;
    }
    .tiles{
        height: 30px;
        width: 30px;
        background-color: #fff;
        color: #242424;
        padding: 1em;
        border: 2px solid #242424;

    }
</style>