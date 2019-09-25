<template>
  <BitmexOI :openinterest="openInterest"></BitmexOI>
</template>

<script>
import BitmexOI from './BitmexOI'

export default {
  components: [
    BitmexOI
  ],
  data: function(){
    return {
      message: [],
      openInterest: [],
      orderBook: []
    }
  },
  mounted(){
    var ws = new WebSocket("wss://www.bitmex.com/realtime")
    var self = this
    ws.onopen = function(){
      ws.send(JSON.stringify({
        op: "subscribe",
        args: ["instrument:XBTUSD", "orderBookL2_25:XBTUSD"]
      }))
    }
    ws.onmessage = function(msg){
      var response = JSON.parse(msg.data)
      self.message.push(response)
      if (response.data[0].openInterest) {
        self.openInterest.push(response.data[0].openInterest)
      }
    } 
  },

}
</script>
