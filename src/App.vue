<template>
  <Todo> <popup />  </Todo>
</template>

<script>
import Todo from './components/Todo.vue';
import popup from './components/popup.vue';

export default {
  name: 'App',
  components: {
    Todo,
    popup,
  },
};
</script>
