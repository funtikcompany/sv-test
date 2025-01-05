<script>
    import { onMount } from 'svelte';
    import { fade, fly } from 'svelte/transition';
    export let showPopup = false;
    export let closePopup = () => {};
  
    let timeRemaining = '00:00:00';
    let timer;
  
    // Таймер
    function updateCountdown() {
      const now = new Date();
      const midnight = new Date();
      midnight.setHours(24, 0, 0, 0);
  
      const diff = midnight - now;
      if (diff <= 0) {
        timeRemaining = '00:00:00';
        return;
      }
  
      const day = Math.floor(diff / (1000 * 60 * 60 * 24));
      const hours = Math.floor(diff / (1000 * 60 * 60));
      const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
      const seconds = Math.floor((diff % (1000 * 60)) / 1000);
  
      timeRemaining =
        String(day).padStart(2, '0') + 'd ' +
        String(hours).padStart(2, '0') + 'h ' +
        String(minutes).padStart(2, '0') + 'm ' +
        String(seconds).padStart(2, '0') + 's';
    }
  
    onMount(() => {
      updateCountdown();
      timer = setInterval(updateCountdown, 1000);
      return () => clearInterval(timer);
    });
  </script>
  
  {#if showPopup}
    <div class="popup-overlay"  in:fade={{ duration: 200 }} out:fade={{ duration: 200 }}>
      <div class="popup-overlay-wrapper"
      in:fly={{ y: 100, duration: 300 }}
      out:fly={{ y: 100, duration: 300 }}>
        <div class="balance">
          <div class="balance-content">
            <img src="/img/Icn_Cmn_Coin.png" alt="">
            <span>500</span>
          </div>
        </div>
  
        <div class="popup-content">
          <div class="popup-body">
            <div class="popup-body-close" on:click={closePopup}>
              <img class="popup-body-cross" src="/img/cross.png" alt="close">
            </div>
  
            <div class="popup-body-header"></div>
  
            <div class="popup-body-content">
              <div class="popup-body-content-wrapper">
                <h2 class="popup-body-content-main-title">
                  <span data-text="Name name">Name name</span>
                </h2>
  
                <div class="countdown">
                  <img src="/img/Icn_Str_Clock.png" alt="clock"> {timeRemaining}
                </div>
  
                <p class="popup-body-content-text">
                  Spin slot <span>MEGALOAD2000</span>at Least 10 times with at least $10 Bet amount least 10 Times with
                </p>
  
                <h3 class="price">
                  <img src="/img/Icn_Cmn_Coin.png" alt="">
                  <span data-text="500/100">500/100</span>
                </h3>
  
                <button class="btn" disabled>
                  <span>Buy</span>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  {/if}

  