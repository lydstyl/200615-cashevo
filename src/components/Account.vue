<template>
  <div class="account">
    <span v-on:click="removeAccount">X</span>
    <h2>
      <input
        class="account-name"
        v-model="newName"
        type="text"
        placeholder="nom"
      />
    </h2>

    <div class="amount">
      <input v-model="newAmount" type="number" placeholder="nouveau montant" />
      <button @click="setAccount">Sauver</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Account",

  props: {
    accountId: Number,
    name: String,
    amount: Number,
  },

  data() {
    return {
      newName: this.name,
      newAmount: this.amount,
    };
  },

  methods: {
    setAccount() {
      this.$emit("setAccount", {
        accountId: this.accountId,
        newName: this.newName,
        newAmount: parseFloat(this.newAmount),
      });
    },

    removeAccount() {
      this.$emit("removeAccount", {
        accountId: this.accountId,
      });
    },
  },
};
</script>

<style scoped>
.account {
  position: relative;
  padding: 20px;
  border: 1px dotted;
}

.account span {
  position: absolute;
  top: -12px;
  right: 0;

  font-size: 2rem;
}

.account span:hover {
  cursor: pointer;
}

h2 {
  font-size: 1.7rem;
  text-align: center;
  margin-bottom: 20px;
}

.account-name {
  width: 100%;
  text-align: center;
}

.amount {
  display: flex;
  justify-content: space-between;
}

input {
  width: 120px;
  margin-right: 20px;
  padding: 2px;
  text-align: right;
  border: none;
}
.amount input {
  color: rgb(255, 99, 132);
}
</style>
