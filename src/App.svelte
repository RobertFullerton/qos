<script>
  import { onMount } from 'svelte';

  import SplashScreen from './components/SplashScreen.svelte';
  // @ts-ignore
  import Scorekeeper from './components/Scorekeeper.svelte';

  let showSplashScreen = true;

  onMount(() => {
    setTimeout(() => {
      showSplashScreen = false;
    }, 4000); // Sets the duration of the splash screen
  });
	
</script>

<style>
 
</style>

{#if showSplashScreen}
  <SplashScreen on:splash-screen-complete={() => showSplashScreen = false} />
{:else}
  <!-- Add your main app content here -->
 <main>
<Scorekeeper />
</main>

{/if}

























