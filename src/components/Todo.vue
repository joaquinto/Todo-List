<template>
  <div class="todo-container">
      <input class="todo-input-field" v-model="state.description" type="text" placeholder="Add Todo" @change="$emit('desc', state.description)"/>
      <ul class="todo-content">
        <li v-for="todo in todos" :key="todo.id">
          <div class="todo">
            <label class="todos" :class="{check : todo.completed}">{{todo.description}}
              <input class="todo-completed" type="checkbox" v-model="todo.completed"/>
              <span class="checkmark"></span>
            </label>
            <div class="todo-action">
              <span class="edit-btn" v-if="!todo.completed" @click="editBtn(todo.id, todo.description)">
            <svg class="edit" width="24" height="24" viewBox="0 0 24 24">
              <path d="M14.06,9L15,9.94L5.92,19H5V18.08L14.06,9M17.66,3C17.41,3 17.15,3.1 16.96,3.29L15.13,5.12L18.88,8.87L20.71,7.04C21.1,6.65 21.1,6 20.71,5.63L18.37,3.29C18.17,3.09 17.92,3 17.66,3M14.06,6.19L3,17.25V21H6.75L17.81,9.94L14.06,6.19Z" />
            </svg>
          </span>
          <span class="trash-btn" @click="deleteTodo(todo.id)">
            <svg class="trash" width="24" height="24" viewBox="0 0 24 24">
              <path d="M9,3V4H4V6H5V19A2,2 0 0,0 7,21H17A2,2 0 0,0 19,19V6H20V4H15V3H9M7,6H17V19H7V6M9,8V17H11V8H9M13,8V17H15V8H13Z" />
            </svg>
          </span>
        </div>
          </div>
        </li>
      </ul>
  </div>
</template>

<script>
import { reactive } from '@vue/composition-api'
  export default {
    props: {
      todos: {
        type: Array,
        required: true
      },
      editBtn: {
        type: Function,
        required: true
      },
      deleteTodo: {
        type: Function,
        required: true
      }
    },
    setup (props) {
      const state = reactive({
        description: ''
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

  .todo-input {
    margin: auto;
    width: 350px;
    padding: 20px;
    border: 2px solid blue;
  }

  .todo-list {
    display: flex;
    border: 2px solid blue;
    align-items: center;
    width: 400px;
  }
  .todo-input-field {
    font-size: 20px;
    width: 350px;
    outline: none;
    border: 2px solid #ccc;
    padding: 5px;
    border-radius: 5px;
  }

  .todo-content {
    padding: 0px;
    list-style-type: none;
  }

  .todo {
    display: flex;
    width: 370px;
    justify-content: space-between;
    align-items: center;
    box-sizing: border-box;
    border-bottom: 1px solid #ccc;
    padding: 5px 20px;
  }

  .todos {
    display: block;
    position: relative;
    padding-left: 35px;
    cursor: pointer;
    font-size: 22px;
  }

  .check {
    text-decoration: line-through;
  }

  .todos input {
    position: absolute;
    opacity: 0;
    cursor: pointer;
    height: 0;
    width: 0;
  }

  .checkmark {
    position: absolute;
    top: 0;
    left: 0;
    height: 25px;
    width: 25px;
    border-radius: 3px;
    background-color: #eee;
  }

  .todos:hover input ~ .checkmark {
    background-color: #ccc;
  }

  .todos input:checked ~ .checkmark {
    background-color: #2196F3;
  }

  .checkmark:after {
    content: "";
    position: absolute;
    display: none;
  }

  .todos input:checked ~ .checkmark:after {
    display: block;
  }

  .todos .checkmark:after {
    left: 9px;
    top: 5px;
    width: 5px;
    height: 10px;
    border: solid white;
    border-width: 0 3px 3px 0;
    -webkit-transform: rotate(45deg);
    -ms-transform: rotate(45deg);
    transform: rotate(45deg);
  }

  .todo-completed {
    width: 25px;
    height: 25px;
    background-color: blue;
  }

  .todo-detail {
    border: 2px solid blue;
  }

  .todo-action {
    display: flex;
    justify-content: space-between;
  }

  .edit-btn {
    cursor: pointer;
    margin-right: 15px;
  }

  .edit {
    fill: blue;
  }

  .trash-btn {
    cursor: pointer;
  }

  .trash {
    fill: red;
  }
</style>
