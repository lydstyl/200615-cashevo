<template>
  <div>
    <hr />
    <h2>id {{ accountId }} Account {{ name }}</h2>

    <input v-model="newAmount" type="number" placeholder="nouveau montant" />
    <p>Le newAmount est : {{ newAmount }}</p>
    <button @click="up">Sauver</button>
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
/* span {
  color: red;
} */
</style>
