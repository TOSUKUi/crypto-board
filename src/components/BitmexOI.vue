<script>
import { Line } from "vue-chartjs";

import "chartjs-plugin-streaming";
export default {
  extends: Line,
  props: ["OI"],
  computed: {
    lastOI: function() {
      return this.OI.slice(-1);
    }
  },
  mounted() {
    var self = this;
    this.renderChart(
      {
        datasets: [
          {
            data: [],
            label: "OpenInterest",
            borderColor: "rgb(255, 99, 132)",
            backgroundColor: "rgba(255, 99, 132, 0.5)",
            fill: false,
            lineTension: 0,
            borderDash: [8, 4]
          }
        ]
      },
      {
        scales: {
          xAxes: [
            {
              type: "realtime",
              realtime: {
                onRefresh: function(chart) {
                  chart.data.datasets[0].data.push({
                    x: Date.now(),
                    y: self.lastOI
                  });
                },
                delay: 0.5,
                duration: 50000
              }
            }
          ]
        }
      }
    );
  }
};
</script>