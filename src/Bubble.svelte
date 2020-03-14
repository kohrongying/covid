<script>
  import { data } from "./data.js";
  import { onMount } from "svelte";
  import Chart from "chart.js";
  onMount(async () => {
		renderChart()
  });
  

  const COLORS = [
    {
      backgroundColor: "#AD94FF33",
      borderColor: "#AD94FF",
      borderWidth: 1,
      hoverBackgroundColor: "#AD94FF66",
      hoverBorderColor: "#AD94FF",
    },
    {
      backgroundColor: "#FF5E5433",
      borderColor: "#FF5E54",
      borderWidth: 1,
      hoverBackgroundColor: "#FF5E5466",
      hoverBorderColor: "#FF5E54",
    },
    {
      backgroundColor: "#99C2FF33",
      borderColor: "#99C2FF",
      borderWidth: 1,
      hoverBackgroundColor: "#99C2FF66",
      hoverBorderColor: "#99C2FF",
    },
    {
      backgroundColor: "#08806433",
      borderColor: "#088064",
      borderWidth: 1,
      hoverBackgroundColor: "#08806466",
      hoverBorderColor: "#088064",
    },
    {
      backgroundColor: "#FF963D33",
      borderColor: "#FF963D",
      borderWidth: 1,
      hoverBackgroundColor: "#FF963D66",
      hoverBorderColor: "#FF963D",
    },
    {
      backgroundColor: "#FF26F333",
      borderColor: "#FF26F3",
      borderWidth: 1,
      hoverBackgroundColor: "#FF26F366",
      hoverBorderColor: "#FF26F3",
    },
  ];

  function renderChart() {
    var ctx = document.getElementById("bubble").getContext("2d");
    var chart = new Chart(ctx, {
      type: "bubble",
      data: {
        datasets: data.global.map((item, index) => {
          return {
            label: item.country,
            data: [{
              x: item.population,
              y: item.infected,
              r: (item.deaths/(Math.log(item.deaths)**2)).toFixed(0),
            }],
            hoverRadius: 0,
            hitRadius: 0,
            radius: 0,
            ...COLORS[index%6]
          }
        })
      },
      options: {
        scales: {
          xAxes: [{
            scaleLabel: {
              display: true,
              labelString: 'Population Size',
            },
            // gridlines: false,
            // type: 'logarithmic',
            ticks: {
              min: 0,
              max: 1500
            }
          }],
          yAxes: [{
            scaleLabel: {
              display: true,
              labelString: '# Infected',
            },
            // type: 'logarithmic',
            // ticks: {
            //   min: 0,
            //   max: 85000
            // }
          }],
        }
      }
    });
  }
</script>

<h2>Global Cases</h2>
<canvas id="bubble"></canvas>
