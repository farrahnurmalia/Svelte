<script>
  export let data;
  export let top;
  export let spacing;
  import { scaleLinear } from 'd3-scale';

  const xScale = scaleLinear()
    .domain([0, 100]) 
    .range([0, 200]); 

  function sum(array, index) {
    return array.slice(0, index).reduce((acc, val) => acc + val, 0);
  }

  function showPercentage(event, percentage) {
    const rect = event.target;
    const rectBounding = rect.getBoundingClientRect();
    const offsetX = event.clientX - rectBounding.left;
    const totalWidth = rectBounding.width;
    const clickedPercentage = Math.round((offsetX / totalWidth) * 100);
    
    const tooltip = document.createElement('div');
    tooltip.classList.add('tooltip');
    tooltip.textContent = `${clickedPercentage}%`;
    tooltip.style.left = `${event.clientX}px`;
    tooltip.style.top = `${event.clientY - 20}px`;
    
    document.body.appendChild(tooltip);

    setTimeout(() => {
      tooltip.remove();
    }, 2000);
  }

  //The percentage for tooltip is shown up, but I still struggle to put it in the place I prefer.
</script>

<div class="brace" style="top: {top}px; left: 100px;">
  <span class="brace-text-before">{data.ageText}</span>
  <span class="brace-opening">{`{`}</span>
  <div class="brace-text-group">
    <span class="brace-text-vertical">{data.text1}</span>
    <svg class="bar-chart" width="200" height="50">
      <!-- Rect elements for the bars -->
      {#each data.percentages1 as percentage, i}
        <rect
          width={xScale(percentage)}
          height="50%"
          fill={data.colors1[i]}
          x={xScale(sum(data.percentages1, i))}
          y="0"
          on:click={(event) => showPercentage(event, percentage)}
        />
      {/each}
    </svg>
    <span class="brace-text-vertical">{data.text2}</span>
    <svg class="bar-chart" width="200" height="50">
      <!-- Rect elements for the bars -->
      {#each data.percentages2 as percentage, i}
        <rect
          width={xScale(percentage)}
          height="50%"
          fill={data.colors2[i]}
          x={xScale(sum(data.percentages2, i))}
          y="0"
          on:click={(event) => showPercentage(event, percentage)}
        />
      {/each}
    </svg>
  </div>
</div>

<style>
.brace {
  position: relative;
  display: inline-block;
  margin: 0 20px;
  top: 20px;
}

.brace-text-before {
  font-size: 17px;
  position: absolute;
  top: 30px;
  left: -100px;
  color: #333;
}

.brace-opening {
  font-size: 80px;
}

.brace-text-group {
  position: relative;
  left: 40px;
  top: -120px;
  margin-top: 20px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.brace-text-vertical {
  font-size: 17px;
  color: #555;
  display: flex;
  align-items: center;
  margin-bottom: 5px;
  margin-left: 10px;
}

.bar-chart {
  padding-left: 0;
  margin-left: 20px;
}

.tooltip {
    position: absolute;
    background-color: rgba(0, 0, 0, 0.8);
    color: white;
    padding: 5px 10px;
    border-radius: 5px;
    font-size: 12px;
  }
</style>
