<template>
  <div id="app">
    <h1>{{ h1Text }} {{ total }}</h1>

    <button type="button" id="addCounter" @click="addNew">
      Add new account
    </button>

    <Account
      v-on:up="up"
      v-for="account in accounts"
      v-bind:key="account.id"
      :accountId="account.id"
      :name="account.name"
      :amount="account.amount"
    ></Account>
  </div>
</template>

<script>
import Account from "./components/Account.vue";

export default {
  name: "App",
  components: {
    Account,
  },

  data() {
    const datas = {
      h1Text: "Le point sur ton cash",
      defaultName: "Account",
      accounts: [
        {
          id: 1,
          name: "CA",
          amount: 1000,
        },
        {
          id: 2,
          name: "Liquide",
          amount: 300,
        },
      ],
    };

    datas.total = datas.accounts.reduce(
      (total, account) => total + account.amount,
      0
    );

    return datas;
  },

  methods: {
    up(evt) {
      this.accounts = this.accounts.map((a) => {
        if (a.id === evt.accountId) {
          return { ...a, amount: evt.newAmount };
        } else {
          return a;
        }
      });

      this.total = this.setTotal();
    },

    addNew() {
      this.accounts.push({
        id: this.accounts.length + 1,
        name: `${this.defaultName} (${this.accounts.length + 1})`,
        amount: 777,
      });

      this.total = this.setTotal();
    },

    setTotal() {
      const total = this.accounts.reduce(
        (total, account) => total + account.amount,
        0
      );

      this.total = total;

      return total;
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
