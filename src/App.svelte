<script>
  import BraceStructure from './BraceStructure.svelte';
  import CircleElements from './CircleElements.svelte';

  const braceData = [
    {
    ageText: 'AGE 15-40',
    text1: 'Germany',
    percentages1: [62.1, 37.3, 0.6],
    colors1: ['#990000', '#FEBE00', '#5B7742'],
    text2: 'Negroes',
    percentages2: [41, 54, 5],
    colors2: ['#990000', '#FEBE00', '#5B7742']
  },
  {
    ageText: '40-60',
    text1: 'Germany',
    percentages1: [10.1, 84.8, 5.1],
    colors1: ['#990000', '#FEBE00', '#5B7742'],
    text2: 'Negroes',
    percentages2: [8.5, 79.5, 12],
    colors2: ['#990000', '#FEBE00', '#5B7742']
  },
  {
    ageText: '60 AND OVER',
    text1: 'Germany',
    percentages1: [9.8, 62.2, 28],
    colors1: ['#990000', '#FEBE00', '#5B7742'],
    text2: 'Negroes',
    percentages2: [4.5, 54.5, 41],
    colors2: ['#990000', '#FEBE00', '#5B7742']
  },
  ];

  const circleDots = [
    { color: 'red', top: 60, left: 50, text: 'SINGLE' },
    { color: 'yellow', top: 120, left: 50, text: 'MARRIED' },
    { color: 'green', top: 80, left: 200, text: 'WIDOWED AND DIVORCED' },
  ];

  // I have tried to declare const adjustBraceData to adjust braceData with scaled values directly but it didn't work. So I commented these codes below. Without these code, I think the scaleLinear doesn't work properly (in the end I still use manual scaling)

  //const adjustedBraceData = braceData.map(data => {
    //return {
      //...data,
      //scaledValues1: data.percentages1.map(percentage => xScale(percentage)),
      //scaledValues2: data.percentages2.map(percentage => xScale(percentage)),
    //};
  //});
</script>

<CircleElements dots={circleDots} />

<div id="braceContainer">
  {#each braceData as data, index}
    <BraceStructure {data} top={60 + index * 240} spacing={0} />
  {/each}
</div>

<style>
  h1 {
    font-family: "Spectral", serif;
    font-weight: 200;
    text-align: center;
    color: rgb(60, 60, 60);
  }

  h1 {
    font-size: 20px;
  }

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

  .brace {
    position: relative;
    display: inline-block;
    margin: 50 20px;
    top: 50px;
  }

  .brace-text-before {
    font-size: 17px;
    position: absolute;
    top: 30px;
    left: -100px;
    color: #333;
  }

  .brace-opening {
    font-size: 70px;
  }

  .brace-text-group {
    position: relative;
    left: 40px;
    top: -110px;
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

</style>
