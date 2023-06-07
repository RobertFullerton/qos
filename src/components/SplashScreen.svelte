<script>

  import { createEventDispatcher } from 'svelte';

  let imageUrl = 'src/assets/img/Splash Design Final New.jpg' 

  export let duration = 5000; // Duration in milliseconds

  const dispatch = createEventDispatcher();


  setTimeout(() => {
    dispatch('splash-screen-complete');
  }, duration);
</script>

<style>
  .img {
    background-size: cover;
    background-position: center;
    height: 100dvh;
    width: 100dvw;
  }
  .loading {
    margin: 0;
    padding: 0;
  position: absolute;
  font-size: 1.5rem;
  font-weight: bold;
  left: 50%;
  bottom: 5%;
  transform: translate(-50%, -50%);
  }

</style>

<figure>
  <img src={imageUrl} alt="background" class="img" />
  <!-- <p aria-busy="true" class="loading">Loading ... </p> -->
</figure>

