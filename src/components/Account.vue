<template>
  <div>
    <hr />
    <h2>Account {{ id }} {{ name2 }} {{ amount2 }}</h2>

    <button @click="up">Up</button>
  </div>
</template>

<script>
export default {
  name: "Account",

  props: ["accountId", "name", "amount"],

  data() {
    return {
      id: this.accountId,
      name2: this.name,
      amount2: this.amount,
    };
  },
  methods: {
    up() {
      this.amount2++;
    },
  },
  computed: {
    // counter() {
    //   let countLen = this.count.toString().length;
    //   let countDiff = this.format - countLen;
    //   let zeros = "";
    //   for (let i = 0; i < countDiff; i++) zeros += "0";
    //   return zeros + this.count;
    // },
  },
};
</script>

<style scoped>
/* span {
  color: red;
} */
</style>
