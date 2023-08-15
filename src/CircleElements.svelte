<script>
  export let dots;
</script>

<div class="graph">
  <div class="title">
    <svg width="500" height="100">
      {#each dots as dot}
        <div class={`dot ${dot.color}`} style={`top: ${dot.top}px; left: ${dot.left}px;`}>
          <span class="dot-text">{dot.text}</span>
        </div>
      {/each}
    </svg>
  </div>
</div>

<style>
  .dot-text {
  margin-left: 30px;
  }

  .dot {
    display: inline-block;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    position: absolute;
  }

  .red {
    background-color: #990000;
  }

  .green {
    background-color: #5B7742;
  }

  .yellow {
    background-color: #FEBE00;
  }
</style>
