<template>
  <div class="inner item card">
    <h1>Todo List</h1>
    <div class="flex col" droppable @dragenter="handleDragEnter">
      <Todo
        v-for="(todo, index) in todos"
        v-bind:todo="{...todo,index}"
        v-bind:key="index"
        v-bind:dragging="dragging && dragIndex === index"
        v-bind:dropping="dragging && dropIndex === index"
        v-on:check="$emit('check', { index , value: $event})"
        v-on:remove="$emit('remove', index)"
        v-on:drag="handleDrag"
      />
    </div>
  </div>
</template>

<script>
import Todo from "./Todo.vue";

export default {
  name: 'TodoList',
  components: {
    Todo,
  },
  props: ['todos'],
  data() {
    return {
      dropIndex: null,
      dragIndex: null,
      dragging: false,
    };
  },
  methods: {
    handleDragEnter(event) {
      const el = event.currentTarget;
      const children = el.children;

      for (let i = 0; i < children.length; i += 1) {
        const rect = children[i].getBoundingClientRect();
        if (event.clientY >= rect.top && event.clientY <= rect.top + rect.height) {
          this.dropIndex = i;
          break;
        }
      }
    },
    handleDrag({ dragIndex, dragging }) {
      this.dragIndex = dragIndex;
      this.dragging = dragging;

      if (!this.dragging && this.dragIndex !== this.dropIndex) {
        this.$emit('swap', { a: this.dragIndex, b: this.dropIndex });
      }
    },
  },
}
</script>

<style scoped>
</style>
