<template>
  <div>
    <hr />
    <h2>{{ accountId }} Account {{ name }} {{ amount }}</h2>

    <!-- <input type="text" v-bind:name="name2" /> -->

    <button @click="up">emit up</button>
  </div>
</template>

<script>
export default {
  name: "Account",

  props: ["accountId", "name", "amount"],

  data() {
    return {
      // name2: this.name,
    };
  },
  methods: {
    up() {
      this.$emit("up", {
        accountId: this.accountId,
        name: this.name,
        amount: this.amount,
        add: 100,
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
