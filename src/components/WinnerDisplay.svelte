<script>
  export let winner;
  export let score;
  export let handsPlayed;
</script>
<style>
  .winner {
    text-align: center;
  }
</style>

<div class="container">
  <h2 class="winner">Winner!</h2>
<div class="grid">
  <h3>{winner.name}</h3>
  <p>Score: {score}</p>
  <p>Hands Played: {handsPlayed}</p>
</div>
</div>