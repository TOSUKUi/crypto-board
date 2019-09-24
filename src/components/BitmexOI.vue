<script>
import { Line } from 'vue-chartjs'

import 'chartjs-plugin-streaming';
export default {
  extends: Line,
  computed: {
    newMessage: function(){
      const last = this.message.slice(-1);
      return last
    },
    lastOI: function(){
      return this.openinterest.slice(-1)
    }
  },
  data : function (){
      return {
        message: [],
        openinterest: []
      }
    },
  mounted () {
    var ws = new WebSocket("wss://www.bitmex.com/realtime")
    var self = this
    ws.onopen = function(){
      ws.send(JSON.stringify({
        op: "subscribe",
        args: ["instrument:XBTUSD"]
      }))
    }
    ws.onmessage = function(msg){
      var response = JSON.parse(msg.data)
      self.message.push(response)
      if (response.data[0].openInterest) {
        self.openinterest.push(response.data[0].openInterest)
      }
    }
    this.renderChart({
      datasets: [{
        data: [],
        label: 'OpenInterest',
        borderColor: 'rgb(255, 99, 132)',
        backgroundColor: 'rgba(255, 99, 132, 0.5)',
        lineTension: 0,
        borderDash: [8, 4]
      }]
    }, {
      scales: {
        xAxes: [{
          type: 'realtime',
          realtime: {
            onRefresh: function(chart) {
              chart.data.datasets[0].data.push({
                x:Date.now(),
                y: self.lastOI,
              })
            },
            delay: 0.5,
            duration: 5000
          }
        }]
      }
    });
  }
}
</script>