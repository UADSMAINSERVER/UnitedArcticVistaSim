<script>
  import { onMount } from "svelte";
  let stage = 0;

  onMount(() => {
    const steps = [1000, 2000, 3000, 4000, 5000, 6000];
    steps.forEach((delay, i) => {
      setTimeout(() => stage = i + 1, delay);
    });

    // Transition to BootManager after final stage
    setTimeout(() => {
      window.location.href = "/boot"; // Replace with router logic
    }, 7000);
  });
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Share+Tech+Mono&display=swap');

  * {
    cursor: none;
  }

  body {
    margin: 0;
    background: black;
    color: #e0e0e0;
    font-family: 'Share Tech Mono', monospace;
    font-size: 1rem;
  }

  .post-container {
    padding: 2rem;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .energy-star {
    text-align: center;
    margin-bottom: 2rem;
  }

  .energy-star img {
    width: 120px;
  }

  .hardware-check {
    margin-top: 2rem;
    border-top: 1px dashed #444;
    padding-top: 1rem;
  }

  .highlight {
    color: #00ff00;
  }
</style>

<div class="post-container">
  <div class="energy-star">
    <img src="/public/icons/energy-star.png" alt="Energy Star Logo" />
  </div>

  {#if stage >= 1}
    <p>Award Modular BIOS v4.51PG, An Energy Star Ally</p>
    <p>Copyright (C) 1984–2025, United Arctic Industries</p>
  {/if}
  {#if stage >= 2}
    <p>UAOS BIOS v.2.0.6</p>
  {/if}
  {#if stage >= 3}
    <p>Main Processor: <span class="highlight">Intel® Pentium® 4 @ 2.80GHz</span></p>
    <p>Memory Testing: <span class="highlight">2097152K OK</span></p>
  {/if}
  {#if stage >= 4}
    <p>Detecting Pri Master ... Virtual Hard Disk C:</p>
    <p>Detecting Pri Slave ... Virtual Hard Disk D:</p>
  {/if}
  {#if stage >= 5}
    <p>Detecting Sec Master ... Virtual CD/DVD E:</p>
    <p>Detecting Sec Slave ... None</p>
  {/if}
  {#if stage >= 6}
    <p>Initializing USB Controllers ... <span class="highlight">Done</span></p>
    <p>Press &lt;DEL&gt; to enter SETUP, &lt;F12&gt; to Boot Menu</p>
  {/if}

  <div class="hardware-check">
    <p><strong>System Check:</strong></p>
    <p>CPU ID: UA-P4-2800</p>
    <p>RAM Slots: 2 × 1024MB DDR2</p>
    <p>GPU: UA Virtual VGA Adapter</p>
    <p>BIOS Integrity: <span class="highlight">Verified</span></p>
  </div>
</div>
