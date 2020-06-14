<template>
  <div id="app">
    <h1>
      CashEvo
      <span>
        {{ total }}
      </span>
    </h1>

    <button class="add-account" @click="addNew">
      Ajouter un compte
    </button>

    <div class="accounts">
      <Account
        v-for="account in accounts"
        v-on:setAccount="setAccount"
        v-on:removeAccount="removeAccount"
        v-bind:key="account.id"
        :accountId="account.id"
        :name="account.name"
        :amount="account.amount"
      />
    </div>

    <button class="add-to-history" @click="addToHistory">
      Ajouter à l'historique
    </button>

    <!-- <pre
      >{{ JSON.stringify(history, null, 4) }}
    </pre> -->

    <FirstChart v-bind:chartData="chartData" v-bind:options="{}" />
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

  mounted() {
    const stored = JSON.parse(localStorage.getItem("cashEvo"));

    Object.keys(stored).forEach((key) => {
      this[key] = stored[key];
    });
  },

  data() {
    const datas = {
      defaultName: "Account",
      accounts: [],

      history: [],

      chartData: {
        labels: [],
        datasets: [
          {
            label: "Historique",
            backgroundColor: "rgba(0, 0, 0, 0)",
            borderColor: "rgb(255, 99, 132)",
            data: [],
          },
        ],
      },
    };

    datas.total = datas.accounts.reduce(
      (total, account) => total + account.amount,
      0
    );

    return datas;
  },

  methods: {
    setAccount(evt) {
      this.accounts = this.accounts.map((a) => {
        if (a.id === evt.accountId) {
          return { ...a, name: evt.newName, amount: evt.newAmount };
        } else {
          return a;
        }
      });

      this.total = this.setTotal();
    },

    removeAccount(evt) {
      this.accounts = this.accounts.filter((a) => a.id !== evt.accountId);

      this.total = this.setTotal();
    },

    addNew() {
      this.accounts.push({
        id: this.accounts.length + 1 + Math.random() * 1000000000000000000,
        name: `${this.defaultName} (${this.accounts.length + 1})`,
        amount: 0,
      });

      this.setTotal();
    },

    setTotal() {
      const total = this.accounts.reduce(
        (total, account) => total + account.amount,
        0
      );

      this.total = total;

      this.saveAllToLocalStorage();

      return total;
    },

    addToHistory() {
      this.history.push({
        id: this.history.length + 1 + Math.random() * 1000000000000000000,
        date: `${new Date().toLocaleString("fr-FR", {
          day: "numeric",
          month: "numeric",
          year: "numeric",
        })}`,
        total: this.total,
      });

      this.setChartData();
    },

    setChartData() {
      this.chartData = {
        labels: this.history.map((h) => h.date),
        datasets: [
          {
            label: "Historique",
            backgroundColor: "rgba(0, 0, 0, 0)",
            borderColor: "rgb(255, 99, 132)",
            data: this.history.map((h) => h.total),
          },
        ],
      };

      this.saveAllToLocalStorage();
    },

    saveAllToLocalStorage() {
      const cashEvo = {
        accounts: this.accounts,
        total: this.total,
        history: this.history,
        chartData: this.chartData,
      };

      localStorage.setItem("cashEvo", JSON.stringify(cashEvo));
    },
  },

  computed: {
    // counter() {
    // },
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  line-height: 1.5;
  margin: 0;
  padding: 0;
  border-radius: 4px;
}

body {
  font-size: 62.5%;
}

input,
button {
  padding: 10px;
  font-size: 1.5rem;
}

button {
  font-size: 1rem;
}

button:hover {
  cursor: pointer;
}

#app {
  max-width: 1200px;
  margin: auto;
  padding: 20px;
}

h1 {
  font-size: 2rem;
  text-align: center;
  margin-bottom: 20px;
}

h1 span {
  color: rgb(255, 99, 132);
}

.add-account {
  display: block;
  margin: 0 auto 50px auto;
}

.accounts {
  display: grid;
  grid-template-columns: repeat(1, 1fr);
  grid-gap: 20px;
  grid-auto-rows: minmax(100px, auto);

  margin-bottom: 50px;
}

.add-to-history {
  margin-bottom: 20px;
}

@media screen and (min-width: 768px) {
  .add-account {
    margin-bottom: 100px;
  }

  .accounts {
    grid-template-columns: repeat(2, 1fr);
    grid-gap: 40px;

    margin-bottom: 100px;
  }
}

@media screen and (min-width: 1200px) {
  .accounts {
    grid-template-columns: repeat(4, 1fr);
  }
}
</style>
