<template lang="pug">
  div
    input(
      v-model="myValue"
      :type="type"
      @keyup.enter="createTask"
    )
</template>

<script>
export default {
  name: 'MyInput',
  props: {
    value: {
      type: String,
      default: '',
    },
    type: {
      type: String,
      default: 'text',
    },
  },
  computed: {
    myValue: {
      get() {
        return this.value;
      },
      set(val) {
        this.$emit('update:value', val);
      },
    },
  },
  methods: {
    createTask() {
      this.$emit('changeCreateTask', this.myValue);
    },
  },
};
</script>
