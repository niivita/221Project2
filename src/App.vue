<template>
  <Todo> <Popup /> <editpopup /> </Todo>
</template>

<script>
import Todo from './components/Todo.vue';
import popup from './components/popup.vue';
import editpopup from './components/editpopup.vue';

export default {
  name: 'App',
  components: {
    Todo,
    popup,
    editpopup,
  },
};
</script>
