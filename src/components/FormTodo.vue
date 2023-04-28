<script>
export default {
  methods: {
    onSubmit() {
      if (this.label === '') {
        return
      }
      this.$emit('todo-added', this.label)
      this.label = ''
    }
  },
  data() {
    return {
      label: ''
    }
  }
}
</script>

<template>
  <form @submit.prevent="onSubmit">
    <input
      type="text"
      id="new-todo-input"
      name="new-todo"
      autocomplete="off"
      v-model.lazy.trim="label"
      class="todo__new-input"
    />
    <button type="submit" class="btn btn__add">Add</button>
  </form>
</template>
