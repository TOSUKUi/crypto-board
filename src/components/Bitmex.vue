<template>
  <div class="layout">
    <BitmexOI v-bind:o-i="openInterest"></BitmexOI>
    {{orderBook}}
  </div>
</template>

<script>
import BitmexOI from "./BitmexOI.vue";

export default {
  components: { BitmexOI },
  data: function() {
    return {
      message: [],
      openInterest: [],
      orderBook: []
    };
  },
  mounted() {
    var ws = new WebSocket("wss://www.bitmex.com/realtime");
    var self = this;
    ws.onopen = function() {
      ws.send(
        JSON.stringify({
          op: "subscribe",
          args: ["instrument:XBTUSD", "orderBookL2_25:XBTUSD"]
        })
      );
    };
    ws.onmessage = function(msg) {
      var response = JSON.parse(msg.data);
      self.message.push(response);
      if (response.data[0].openInterest) {
        self.openInterest.push(response.data[0].openInterest);
      }
      if (response.table == "orderBookL2_25") {
        updateOrderBook(response.data, response.action);
      }
    };

    function nextOrderBook(data, action) {
      console.log(action);
      switch (action) {
        case "partial":
          self.orderBook = data;
          break;
        case "update":
          self.orderBook = updateOrderBook(self.orderBook, data);
          break;
      }
    }

    function updateOrderBook(orderBook, newOrderBook) {
      var updatedOrderBook = orderBook;
      orderBook.forEach(function(oldOrd, i) {
        newOrderBook.forEach(newOrd => {
          if (oldOrd.id == newOrd.id) {
            updatedOrderBook[i] = newOrd;
          }
        });
      });
      return updatedOrderBook;
    }
  }
};
</script>
