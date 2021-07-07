<template lang="pug">
  div
    input(
      v-model="myValue"
      :type="type"
      @keyup.enter="createTask"
    )
    div(
      v-if="!valid"
    ).task-page__error Мин символов {{minSymbol}}
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
    minSymbol: {
      type: Number,
      default: 3,
    },
  },
  data: () => ({
    valid: true,
  }),
  computed: {
    myValue: {
      get() {
        return this.value;
      },
      set(val) {
        this.valid = (val.length < this.minSymbol) ? false : 'true';
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
<style lang="sass">
  .task-page__error
    color: red
</style>
