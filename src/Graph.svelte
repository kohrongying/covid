<script>
  import { data } from "./data.js";
  import { onMount } from "svelte";
  import Chart from "chart.js";
  onMount(async () => {
		renderChart()
	});

  function renderChart() {
    var ctx = document.getElementById("myChart").getContext("2d");
    var chart = new Chart(ctx, {
      type: "line",
      data: {
        labels: data.general.map(item => item.date),
        datasets: [
          {
            label: "Total Discharged",
            backgroundColor: "#5CEBFF",
            borderColor: "#5CEBFF",
            data: data.general.map(item => item.totalDischarged)
          },
          {
            label: "Total Infected",
            backgroundColor: "rgb(255, 99, 132)",
            borderColor: "rgb(255, 99, 132)",
            data: data.general.map(item => item.totalCases)
          },
        ]
      },
      options: {
        xAxes: [{
          type: 'time',
          time: {
            unit: 'month',
            displayFormats: {
                quarter: 'll'
            }
          }
        }]
      }
    });
  }
</script>

<h2>Singapore COVID Cases</h2>
<canvas id="myChart"></canvas>