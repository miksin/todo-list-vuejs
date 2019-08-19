<template>
  <div
    class="item card flex row align-center"
    :class="[borderClass]"
    draggable
    @dragstart="handleDragStart"
    @dragend="handleDragEnd"
  >
    <div
      :class="[todo.done ? 'checked' : 'unchecked', 'checkbox', 'line-size']"
      @click="handleCheck(!todo.done)"
    ></div>
    <h3 class="title" v-bind:class="[todo.done ? 'del-line' : '']">
      {{ todo.title }}
    </h3>
    <h3 class="grow-1 content" :class="[todo.done ? 'del-line' : '']">{{ todo.description }}</h3>
    <div class="line-size" @click="handleRemove">
      <img style="width: 100%; height: 100%" src="../assets/delete.svg" alt="">
    </div>
  </div>
</template>

<script>
export default {
  name: 'Todo',
  props: ['todo', 'dragging', 'dropping'],
  methods: {
    handleCheck(value) {
      this.$emit('check', value);
    },
    handleDragStart() {
      this.$emit('drag', { dragIndex: this.todo.index, dragging: true });
    },
    handleDragEnd() {
      this.$emit('drag', { dragIndex: this.todo.index, dragging: false });
    },
    handleRemove() {
      this.$emit('remove');
    }
  },
  computed: {
    borderClass() {
      return this.dropping ? 'dropping' : this.dragging ? 'dragging' : '';
    },
  },
}
</script>

<style scoped>
.card:hover {
  background-color: #eeeeee;
}

.title {
  margin-right: 12px;
}

.content {
  text-align: left;
  color: #a1a1a1;
}

.del-line {
  text-decoration: line-through;
}

.line-size {
  width: 24px;
  height: 24px;
}

.dragging > * {
  visibility: hidden;
}
.dragging {
  border: 1px dashed #2196f3;
  box-shadow: none;
}
.dropping {
  border: 1px dashed #ff215c;
  box-shadow: none;
}
</style>
