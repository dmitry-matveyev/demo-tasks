<template lang="pug">
  button(
    @click="backToHome"
  ) Back
</template>

<script>
export default {
  name: 'BackButton',
  methods: {
    backToHome() {
      this.$router.push({ name: 'Home' });
    },
  },
};
</script>
