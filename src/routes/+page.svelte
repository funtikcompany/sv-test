<script>
  import Popup from '$lib/Popup.svelte';
  import "../app.css";

  let showPopup = false;

  function openPopup() {
    showPopup = true;
  }

  function closePopup() {
    showPopup = false;
  }
</script>

<div class="container">
  <button on:click={openPopup} class="open-button">Open Popup</button>
</div>

<Popup
  showPopup={showPopup}
  closePopup={closePopup}
/>

<style>
</style>
