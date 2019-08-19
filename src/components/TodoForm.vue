<template>
  <div class="inner card flex col">
    <div class="flex col align-start">
      <h4 class="form title">Title</h4>
      <input v-model="titleText" class="form input" type="text" name="title" id="title" />
    </div>
    <div class="item flex col align-start">
      <h4 class="form title">Description</h4>
      <input v-model="descriptionText" class="form input" type="text" name="description" id="description" />
    </div>
    <div class="item flex row just-center align-center">
      <button v-on:click="submit()" class="item btn filled fullsize">Create</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TodoForm',
  data() {
    return {
      titleText: '',
      descriptionText: '',
    };
  },
  methods: {
    submit() {
      const title = this.titleText.trim();
      const description = this.descriptionText.trim();
      if (title.length > 0) {
        this.$emit('add-todo', {
          title,
          description,
          done: false,
        });
      }
      this.titleText = '';
      this.descriptionText = '';
    },
  },
}
</script>

<style scoped>
.form.title {
  margin: 8px 0;
}
.form.input {
  width: 100%;
  padding: 8px;
  border-radius: 5px;
  outline: none;
  box-shadow: none;
  border: 1px solid #424242;
}
</style>