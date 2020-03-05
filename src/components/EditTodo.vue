<template>
  <div class="todo-container">
    <div class="edit-view">
      <h2>Edit Todo </h2>
      <input class="edit-input" type="text" v-model="state.editDescription">
      <div class="ca">
        <button class="btn save-btn" @click="$emit('editTodo', state.todoId, state.editDescription)">
          Save
        </button>
        <button class="btn cancel-btn" @click="cancelBtn">
          Cancel
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive } from '@vue/composition-api'
  export default {
    name: 'edit-todo',
    props: {
      todoId: {
        type: Number,
        required: true
      },
      editDescription: {
        type: String,
        required: true
      },
      cancelBtn: {
        type: Function,
        required: true
      }
    },
    setup (props) {
      const state = reactive({
        editDescription: props.editDescription,
        todoId: props.todoId
      })
      return {
        state
      }
    }
  }
</script>

<style>
  .todo-container{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-top: 20px;
  }
  .edit-view {
    display: flex;
    flex-direction: column;
  }

  .edit-input {
    font-size: 20px;
    width: 350px;
    outline: none;
    border: 2px solid #ccc;
    padding: 5px;
    border-radius: 5px;
    margin-bottom: 20px;
  }

  .ca {
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .btn {
    width: 100px;
    height: 40px;
    border: none;
    font-size: 18px;
    border-radius: 5px;
  }

  .save-btn {
    background-color: green;
    color: white;
    margin-right: 20px;
    cursor: pointer;
  }

  .cancel-btn {
    cursor: pointer;
  }
</style>
