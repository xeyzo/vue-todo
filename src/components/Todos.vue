<template lang="html">
  <section class="collection">
    <template class="collection-item" v-for="todo in todos">
      <TodoItem :todo="todo" @del-todo="$emit('del-todo', todo.id)"/>
    </template>
  </section>
</template>

<script>
import TodoItem from './TodoItem'

export default {
  name: "Todos",
  props: ["todos"],
  components: {
    TodoItem
  }
}
</script>

<style lang="css" scoped>
.collection {
  border: none;
}
</style>
