<template>
  <div id="app">
    <input v-model="cPrice" type="number" />
    <input v-model="cQty" type="number" />
    <input v-model="cAmount" type="number" />
    <button @click="submit">submit</button>
    <br />
    <div style="display: flex; justify-content: space-between">
      <label>{{ cPrice }}</label>
      <label>{{ cQty }}</label>
      <label>{{ cAmount }}</label>
      <label>{{ cJson }}</label>
    </div>
    <div>
      <div v-for="item in log" :key="item">
        <label> {{ item }} </label>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  components: {},
  data() {
    return {
      price: 0,
      qty: 0,
      amount: 0,
      nonce: 0,
      log: [],
      cJson: "",
    };
  },
  computed: {
    cPrice: {
      get: function () {
        return this.price;
      },
      set: function (val) {
        this.log.unshift(`edit price | new price: ${val}`);
        this.price = val;
      },
    },
    cQty: {
      get: function () {
        return this.qty;
      },
      set: function (val) {
        this.log.unshift(`edit qty | new qty: ${val}`);
        this.qty = val;
      },
    },
    cAmount: {
      get: function () {
        return this.amount;
      },
      set: function (val) {
        this.log.unshift(`edit amount | new amount: ${val}`);
        this.amount = val;
      },
    },
    cNonce: {
      get: function () {
        return this.nonce;
      },
      set: function (val) {
        this.log.unshift(`edit nonce | new nonce: ${val}`);
        this.nonce = val;
      },
    },
  },
  methods: {
    submit: function () {
      this.cNonce++;
      if (this.cAmount % 2 !== 0) {
        this.log.unshift(`amount: ${this.cAmount} is not a an even number`);
        return;
      }
      setTimeout(() => {
        localStorage.setItem(
          "data",
          JSON.stringify({
            price: this.price,
            qty: this.qty,
            amount: this.amount,
            nonce: this.nonce,
          })
        );
        this.log.unshift(`new data success writed`);
        this.cJson = localStorage.getItem("data") || "";
      }, 1000);
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
