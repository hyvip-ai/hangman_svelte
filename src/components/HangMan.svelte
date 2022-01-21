<script>
  export let wrongWords = [];
</script>

<div class="man">
  <svg height="250" width="200" class="figure-container">
    <!-- Rod -->
    <line x1="60" y1="20" x2="140" y2="20" class="figure_part" />
    <line x1="140" y1="20" x2="140" y2="50" class="figure_part" />
    <line x1="60" y1="20" x2="60" y2="230" class="figure_part" />
    <line x1="20" y1="230" x2="100" y2="230" class="figure_part" />

    <!-- Head -->
    <circle
      cx="140"
      cy="70"
      r="20"
      class:figure_part={wrongWords.length >= 1}
    />
    <!-- Body -->
    <line
      x1="140"
      y1="90"
      x2="140"
      y2="150"
      class:figure_part={wrongWords.length >= 2}
    />
    <!-- Arms -->
    <line
      x1="140"
      y1="120"
      x2="120"
      y2="100"
      class:figure_part={wrongWords.length >= 3}
    />
    <line
      x1="140"
      y1="120"
      x2="160"
      y2="100"
      class:figure_part={wrongWords.length >= 4}
    />
    <!-- Legs -->
    <line
      x1="140"
      y1="150"
      x2="120"
      y2="180"
      class:figure_part={wrongWords.length >= 5}
    />
    <line
      x1="140"
      y1="150"
      x2="160"
      y2="180"
      class:figure_part={wrongWords.length >= 6}
    />
  </svg>
</div>

<style>
  .figure-container {
    fill: transparent;
    stroke: #fff;
    stroke-width: 4px;
    stroke-linecap: round;
  }
  .figure-container circle,
  .figure-container line {
    display: none;
  }
  .figure_part {
    display: inline-block !important;
  }
</style>
