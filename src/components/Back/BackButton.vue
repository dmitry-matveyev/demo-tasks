<template lang="pug">
  button(
    class="task-page__create"
    @click="back"
  ) Назад
</template>

<script>
export default {
  name: 'BackButton',
  methods: {
    back() {
      this.$router.push({ name: 'Home' });
    },
  },
};
</script>

<style scoped>

</style>
