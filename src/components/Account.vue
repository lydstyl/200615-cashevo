<template>
  <div>
    <hr />
    <h2>{{ name }}</h2>

    <input v-model.number="amount" />
    <p>Le amount est : {{ amount }}</p>
  </div>
</template>

<script>
export default {
  name: "Account",
  props: {
    name: String,
    // amount: String,
  },
  data: () => {
    return { amount: 2000 };
  },
};
</script>

<style scoped>
p {
  color: red;
}
</style>
