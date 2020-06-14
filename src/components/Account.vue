<template>
  <div class="account">
    <h2>{{ name }}</h2>

    <div class="amount">
      <input v-model="newAmount" type="number" placeholder="nouveau montant" />
      <button @click="up">Sauver</button>
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
      newAmount: this.amount,
    };
  },

  methods: {
    up() {
      this.$emit("up", {
        accountId: this.accountId,
        newAmount: parseFloat(this.newAmount),
      });
    },
  },
  computed: {
    // counter() {
    // },
  },
};
</script>

<style scoped>
.account {
  padding: 20px;
  border: 1px dotted;
}

h2 {
  font-size: 1.7rem;
  text-align: center;
  margin-bottom: 20px;
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
</style>
