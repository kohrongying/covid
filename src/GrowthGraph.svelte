<script>
  import { data } from "./data.js";
  import { onMount } from "svelte";
  import Chart from "chart.js";
  onMount(async () => {
		renderChart()
	});

  function renderChart() {
    var ctx = document.getElementById("myChart2").getContext("2d");
    var chart = new Chart(ctx, {
      type: "line",
      data: {
        labels: data.general.map(item => item.date),
        datasets: [
          {
            label: "Discharged Cases",
            backgroundColor: "transparent",
            borderColor: "#5CEBFF",
            data: data.general.map(item => item.newDischarged)
          },
          {
            label: "New Cases",
            backgroundColor: "transparent",
            borderColor: "rgb(255, 99, 132)",
            data: data.general.map(item => item.newCases)
          },
        ]
      },
      options: {}
    });
  }
</script>
<h2>Growth of Singapore COVID Cases</h2>
<canvas id="myChart2"></canvas>
