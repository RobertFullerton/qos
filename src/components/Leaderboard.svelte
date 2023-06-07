<script>
  export let leaderboardData;
</script>
<style>
  .leaderboard {
    text-align: center;
  }
</style>
<div class="container">
<h2 class="leaderboard">Leaderboard</h2>
{#each leaderboardData as item, index}
<div class="grid">
  
  
    <p>Date: {item.date}</p>
      {#each item.winners as winner}
                <p>{winner.name}</p>
                <p>Score: {winner.score}</p>
                <p>Hands Won: {winner.handsWon}</p>
            
            {/each}
          </div>
      {/each}

   
 

</div>
