<script>

import { Line } from 'vue-chartjs'

import 'chartjs-plugin-streaming';


export default {
  extends: Line,
  mounted () {
      this.renderChart({
      datasets: [{
        data: [],
        label: 'Dataset 1',
        borderColor: 'rgb(255, 99, 132)',
        backgroundColor: 'rgba(255, 99, 132, 0.5)',
        lineTension: 0,
        borderDash: [8, 4]
      }, {
        data: [],
        label: 'Dataset 2',
        borderColor: 'rgb(54, 162, 235)',
      }]
    }, {
      scales: {
        xAxes: [{
          type: 'realtime',
          realtime: {
            onRefresh: function(chart) {
              chart.data.datasets.forEach(function(dataset) {
                dataset.data.push({
                  x:Date.now(),
                  y:Math.random()
                });
              });
            },
            delay: 0.3,
            duration:15000 
          }
        }]
      }
    });
  }
}
</script>