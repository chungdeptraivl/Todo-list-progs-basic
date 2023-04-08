<template>
  <div id="root">
    <list-student />
    <todo-list />
  </div>
</template>

<script>
import ListStudent from '~/components/ListStudent.vue'
import TodoList from '~/components/TodoList.vue'
export default {
  components: { ListStudent, TodoList },
}
</script>

<style></style>
