<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    id: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      newTitle: this.title
    }
  },
  methods: {
    onSubmit() {
      if (this.newTitle && this.newTitle !== this.title) {
        this.$emit('item-edited', this.newTitle)
      }
    },
    onCancel() {
      this.$emit('edit-cancelled')
    }
  },
  mounted() {
    const labelInputRef = this.$refs.labelInput
    labelInputRef.focus()
  }
}
</script>

<template>
  <form class="todo__edit-form" @submit.prevent="onSubmit">
    <div>
      <label class="todo__edit-label">Edit </label>
      <input
        :id="id"
        class="todo__edit-input"
        ref="labelInput"
        type="text"
        autocomplete="off"
        v-model.lazy.trim="newTitle"
      />
    </div>
    <div class="todo__btn-group">
      <button type="button" class="btn" @click="onCancel">Cancel</button>
      <button type="submit" class="btn btn__save">Save</button>
    </div>
  </form>
</template>
