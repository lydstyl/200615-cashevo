<template>
  <div id="app">
    <h1>CashEvo {{ total }}</h1>

    <button class="add-account" type="button" id="addCounter" @click="addNew">
      Add new account
    </button>

    <div class="accounts">
      <Account
        v-on:up="up"
        v-for="account in accounts"
        v-bind:key="account.id"
        :accountId="account.id"
        :name="account.name"
        :amount="account.amount"
      ></Account>
    </div>

    <FirstChart></FirstChart>
  </div>
</template>

<script>
import Account from "./components/Account.vue";
import FirstChart from "./components/FirstChart.vue";

export default {
  name: "App",
  components: {
    Account,
    FirstChart,
  },

  data() {
    const datas = {
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
        amount: 0,
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
  max-width: 1200px;
  margin: auto;
}

h1 {
  text-align: center;
}

.add-account {
  display: block;
  margin: 0 auto 50px auto;
}

@media screen and (min-width: 768px) {
  .add-account {
    margin-bottom: 100px;
  }
}

.accounts {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 20px;
  grid-auto-rows: minmax(100px, auto);

  margin-bottom: 50px;
}

@media screen and (min-width: 768px) {
  .accounts {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 40px;

    margin-bottom: 100px;
  }
}

@media screen and (min-width: 1200px) {
  .accounts {
    display: grid;
    grid-template-columns: repeat(7, 1fr);
    grid-gap: 40px;
  }
}
</style>
