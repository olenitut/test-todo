<script>
import editTodo from './EditTodo.vue'

export default {
  components: {
    editTodo
  },

  props: {
    title: { required: true, type: String },
    completed: { default: false, type: Boolean },
    id: { required: true, type: Number }
  },

  data() {
    return {
      isEditing: false
    }
  },

  computed: {
    isCompleted() {
      return this.completed
    }
  },

  methods: {
    deleteToDo() {
      this.$emit('item-deleted')
    },

    showForm() {
      this.isEditing = true
    },

    itemEdited(newTitle) {
      this.$emit('item-edited', newTitle)
      this.isEditing = false
      this.focusOnEditButton()
    },
    editCancelled() {
      this.isEditing = false
      this.focusOnEditButton()
    },
    focusOnEditButton() {
      this.$nextTick(() => {
        const editButtonRef = this.$refs.editButton
        editButtonRef.focus()
      })
    }
  }
}
</script>

<template>
  <div class="todo__item" v-if="!isEditing">
    <div class="todo__checkbox-box">
      <input
        type="checkbox"
        class="todo__checkbox"
        :id="id"
        :checked="isCompleted"
        @change="$emit('status-changed')"
      />
      <label :for="id" class="todo__checkbox-label">{{ title }}</label>
    </div>
    <div class="todo__btn-group">
      <button type="button" class="btn" ref="editButton" @click="showForm">Edit</button>
      <button type="button" class="btn btn__delete" @click="deleteToDo">Delete</button>
    </div>
  </div>
  <edit-todo
    v-else
    :id="id"
    :title="title"
    @item-edited="itemEdited"
    @edit-cancelled="editCancelled"
  ></edit-todo>
</template>
