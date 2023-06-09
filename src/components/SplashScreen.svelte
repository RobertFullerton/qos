<script>
import image from '../assets/img/SplashDesignFinal.jpg'
  import { createEventDispatcher } from 'svelte';

  let imageUrl = image;
  let year = new Date().getFullYear();

  // export let duration = 2000; // Duration in milliseconds

  // const dispatch = createEventDispatcher();


  // setTimeout(() => {
  //   dispatch('splash-screen-complete');
  // }, duration);
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
  font-size: .75rem;
  font-weight: bold;
  left: 50%;
  bottom: 5%;
  transform: translate(-50%, -50%);
  }

</style>


  <img src={imageUrl} alt="background" class="img" />
  <p class="loading"> QOS &copy; {year} </p>

