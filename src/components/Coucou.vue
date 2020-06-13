<template>
  <div>
    <hr />

    <span>coucou {{ firstName }}</span>

    <input type="number" />
  </div>
</template>

<script>
export default {
  name: "Coucou",
  props: {
    firstName: String,
  },
};
</script>

<style scoped>
span {
  color: red;
}
</style>
