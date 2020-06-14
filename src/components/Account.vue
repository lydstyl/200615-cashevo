<template>
  <div class="account">
    <h2>{{ name }}</h2>

    <div class="amount">
      <input v-model="newAmount" type="number" placeholder="nouveau montant" />
      <!-- <p>Le newAmount est : {{ newAmount }}</p> -->
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
  border: 1px dotted;
}

h2 {
  text-align: center;
}

.amount {
  display: flex;
  justify-content: space-between;
}

input {
  max-width: 52px;
}
</style>
