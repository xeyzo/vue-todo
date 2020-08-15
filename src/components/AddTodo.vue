<template lang="html">
  <div class="">
    <form @submit="addTodo">
      <input type="text" v-model="title" name="title" placeholder="Add todo...">
      <input type="submit" value="Add Todo">
    </form>
  </div>
</template>

<script>
export default {
  name: 'AddTodo',
  data() {
    return {
      title: ''
    }
  },
  methods: {
    addTodo(e) {
      const newTodo = {
        title: this.title,
        completed: false
      }

      this.$emit('add-todo', newTodo);
      this.title = '';
      e.preventDefault();
    }
  }
}
</script>

<style lang="css" scoped>
</style>
