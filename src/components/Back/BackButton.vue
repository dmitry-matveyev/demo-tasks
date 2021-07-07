<template lang="pug">
  a(
    class="task-page__back"
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

<style lang="sass">
.task-page__back
  font-size: 25px
.task-page__back:hover
  cursor: pointer
</style>
