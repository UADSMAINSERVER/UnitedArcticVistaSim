<script>
  import { onMount } from "svelte";

  let selectedOption = 0;
  let countdown = 10;
  let booting = false;

  const options = [
    "Start Windows Vista Simulator",
    "Reinstall Windows Vista Simulator"
  ];

  function handleKeydown(event) {
    if (event.key === "ArrowDown") {
      selectedOption = (selectedOption + 1) % options.length;
    } else if (event.key === "ArrowUp") {
      selectedOption = (selectedOption - 1 + options.length) % options.length;
    } else if (event.key === "Enter") {
      booting = true;
      // Trigger next screen logic here
    } else if (event.key === "Escape") {
      location.reload(); // Simulate restart
    }
  }

  onMount(() => {
    window.addEventListener("keydown", handleKeydown);
    const timer = setInterval(() => {
      if (countdown > 0) countdown--;
      else {
        clearInterval(timer);
        booting = true;
        // Trigger auto-boot logic here
      }
    }, 1000);
  });
</script>

<style>
  * {
    cursor: none;
  }

  body {
    margin: 0;
    background: black;
    color: white;
    font-family: "Segoe UI", sans-serif;
  }

  .boot-container {
    padding: 2rem;
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .instructions {
    margin-bottom: 1rem;
    font-size: 1rem;
  }

  .option {
    padding: 0.5rem 1rem;
    margin: 0.3rem 0;
    font-size: 1.1rem;
  }

  .option.selected {
    background: white;
    color: black;
    font-weight: bold;
  }

  .footer {
    margin-top: 2rem;
    font-size: 0.9rem;
    color: gray;
  }
</style>

<div class="boot-container">
  <div class="instructions">
    <p>Use the ↑ and ↓ keys to move the selection.</p>
    <p>Press ENTER to boot the selected OS, or ESC to restart.</p>
    <p><strong>PLEASE SELECT AN OPTION:</strong></p>
  </div>

  {#each options as option, i}
    <div class="option {selectedOption === i ? 'selected' : ''}">
      {option}
    </div>
  {/each}

  <div class="footer">
    <p>Auto-booting in {countdown} seconds...</p>
  </div>
</div>
