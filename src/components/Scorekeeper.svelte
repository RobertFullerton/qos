<script>
    import { onMount } from 'svelte';
  
    import SplashScreen from '../components/SplashScreen.svelte';
    import WinnerDisplay from '../components/WinnerDisplay.svelte';
    import Leaderboard from '../components/Leaderboard.svelte';
    import NewGameButton from '../components/NewGameButton.svelte';
  
    let showSplashScreen = true;
  
    onMount(() => {
      setTimeout(() => {
        showSplashScreen = false;
      }, 4000); // Sets the duration of the splash screen
    });
      
       let players = [];
  
    let rows = [[]];
  
    let newPlayerName = '';
  
    let leaderboardData = [];
      
         function addPlayer() {
      if (players.length < 5) {
        players = [...players, { name: newPlayerName[0].toUpperCase()+ newPlayerName.substring(1)}];
        newPlayerName = '';
      }
    }
  
    function addRow() {
      const newRow = new Array(players.length).fill(0);
      rows = [...rows, newRow];
    }
  
    function updateScore(playerIndex, rowIndex, event) {
      const score = parseInt(event.target.value);
      rows[rowIndex][playerIndex] = isNaN(score) ? 0 : score;
      rows = [...rows]; // Trigger reactivity
    }
  
    function resetGame() {
      players = [];
      rows = [[]];
          totalScores = [];
    }
  
    let totalScores = [];
  
    let winnerData;
  
  
    $: {
      calculateTotalScores();
      let winningIndex = totalScores.findIndex(score => score >= 1000);
      if (winningIndex !== -1) {
        const winner = players[winningIndex];
        const winnerScore = totalScores[winningIndex];
        const handsPlayed = rows.length;
  
        winnerData = {
          winner,
          score: winnerScore,
          handsPlayed
        };
  
        const currentDate = new Date().toLocaleDateString();
        const leaderboardItem = {
          date: currentDate,
          winners: [
            {
              name: winner.name,
              score: winnerScore,
              handsWon: handsPlayed
            }
          ]
        };
        leaderboardData = [leaderboardItem, ...leaderboardData];
      } else {
        winnerData = null;
      }
    }
  
    function calculateTotalScores() {
      totalScores = players.map((player, playerIndex) => {
        return rows.reduce((sum, row) => {
          return sum + (row[playerIndex] || 0);
        }, 0);
      });
    }
  </script>
  
  <style>
    button {
      width: auto;
      padding: 5px;
      font-size: 1rem;
    }
    .container {
      margin-top: 10%;
    }
    .grid {
      margin: 0 auto;
    }
   
    .newGameButton {
      padding: 20px ;
    }
    td {
      padding: 3px;
    }
  
    .totalScore {
      font-size: 1.5rem;
      font-weight: bold;
      text-align: center;
    }
    .scoreboard {
      text-align: center;
      margin-top: 10%;
    }
  
   
  </style>
  
  {#if showSplashScreen}
    <SplashScreen on:splash-screen-complete={() => showSplashScreen = false} />
  {:else}
    <!-- Add your main app content here -->
   <main>
  
     <div class="container">
        <div class="grid">
          <input bind:value={newPlayerName} type="text" placeholder="Player Name" />
          <button on:click={addPlayer} class="addPlayerBtn">Add Player</button>
        </div>
      <section> 
        <h1 class="scoreboard">
           Scoreboard
        </h1>
    <table>
          <thead>
        <tr>
          {#each players as player, index}
            <th>{player.name}</th>
          {/each}
        </tr>
      </thead>
      <tbody>
        {#each rows as row, rowIndex}
          <tr  key={rowIndex}>
            {#each players as player, playerIndex}
              <td  key={playerIndex}>
                <input type="number" min="-1000" value={row[playerIndex]} on:input={event => updateScore(playerIndex, rowIndex, event)} />
              </td>
            {/each}
          </tr>
        {/each}
        <tr>
          {#each totalScores as totalScore, playerIndex}
            <td class="totalScore" key={playerIndex}>{totalScore}</td>
          {/each}
        </tr>
        <div>
          <button on:click={addRow}>Next Hand</button>
      </div>
      </tbody>
    </table>
  </section>
    {#if winnerData}
      <WinnerDisplay
        winner={winnerData.winner}
        score={winnerData.score}
        handsPlayed={winnerData.handsPlayed}
      />
    {/if}
  
    
    <Leaderboard {leaderboardData} />
  
    <div class="newGameButton">
      <NewGameButton {resetGame} />
    </div>
  </main>
  
  {/if}
    