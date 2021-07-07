<template lang="pug">
  div
    div.display_flex
      BackButton
      h1 Creating new task

    div.task-page__info Title:
      MyInput(
        :value.sync="task.title"
        @changeCreateTask="createTask"
      )

    div.task-page__info Description:
      MyInput(
        :value.sync="task.description"
        @changeCreateTask="createTask"
      )

    button.task-page__create(
      @click="createTask"
      :disabled="!disabled"
    ) Create Task
</template>

<script>
export default {
  name: 'NewTask',

  components: {
    MyInput: () => import('@/components/Input/MyInput.vue'),
    BackButton: () => import('@/components/Back/BackButton.vue'),
  },
  data() {
    return {
      task: {
        title: '',
        description: '',
        status: 1,
        created_date: null,
      },
    };
  },
  computed: {
    disabled() {
      return this.task.title.length >= 3 && this.task.description.length >= 3;
    },
  },
  methods: {
    async createTask() {
      const date = new Date();
      this.task.created_date = date.toJSON();

      this.$emit('changeLoadingState', true);

      await fetch('http://localhost:3000/tasks', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify(this.task),
      })
        .then((response) => {
          if (!response.ok) {
            this.$emit('changeLoadingState', false);

            this.$router.push({ path: '/error/' });
            throw response;
          }

          return response.json();
        })
        .then((data) => {
          this.$emit('changeLoadingState', false);

          this.$emit('createTask', data);
          this.$router.replace({ path: `/tasks/${data.id}` });
        });
    },
  },
};
</script>

<style lang="sass">

</style>
