<template>
  <div id="app">
    <section>
      <h1>Lorem Ipsum Dolor Sit Amet</h1>
      <div class="formcontainer">
        <hr />
        <div class="container">
          <label for="uname">
            <strong>Full Name</strong>
          </label>
          <input v-model="full_name" required type="text" placeholder="John Doe" name="uname" />
          <label for="email">
            <strong>Email Address</strong>
          </label>
          <input v-model="email" required type="text" placeholder="customer@email.com" name="email" />
          <label for="amount">
            <strong>Amount</strong>
          </label>
          <input v-model.number="amount" type="number" placeholder="1000" name="amount" required />
          <br />
          <br />
          <paystack
            :amount="amount * 100"
            :email="email"
            :paystackkey="PUBLIC_KEY"
            :reference="reference"
            :callback="processPayment"
            :close="close"
            :embed="false"
          >
            <i class="fas fa-money-bill-alt"></i>
            Make Payment
          </paystack>
        </div>
      </div>
    </section>
    <img style="max-width:200px;" alt="Vue logo" src="./assets/pstk.png" />
  </div>
</template>

<script>
import paystack from "vue-paystack";
export default {
  name: "App",
  components: {
    paystack
  },
  computed: {
  
    reference() {
      let text = "";
      let possible =
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";

      for (let i = 0; i < 10; i++)
        text += possible.charAt(Math.floor(Math.random() * possible.length));

      return text;
    }
  },
  methods: {
    processPayment: () => {
      window.alert("Payment recieved")
    },
    close: () => {
     console.log("You closed checkout page")
    }
  },
  data: () => {
    return {
      amount: 0,
      full_name: '',
      email: '',
      PUBLIC_KEY: "YOUR_PAYSTACK_PUBLIC_KEY"
    };
  }
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
html,
body {
  display: flex;
  justify-content: center;
  font-family: Roboto, Arial, sans-serif;
  font-size: 15px;
}

input {
  width: 100%;
  padding: 16px 8px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  box-sizing: border-box;
}
button {
  background-color: #8ebf42;
  color: white;
  padding: 14px 0;
  margin: 10px 0;
  border: none;
  cursor: grabbing;
  width: 100%;
}

button:hover {
  opacity: 0.8;
}
.formcontainer {
  text-align: left;
  margin: 24px 50px 12px;
}
.container {
  padding: 16px 0;
  text-align: left;
}
span.psw {
  float: right;
  padding-top: 0;
  padding-right: 15px;
}
/* Change styles for span on extra small screens */
@media screen and (max-width: 300px) {
  span.psw {
    display: block;
    float: none;
  }
}
</style>
