<template>
  <div>
    <Todo v-if="!state.edit"
    :todos="state.todos"
    :editBtn="editBtn"
    :deleteTodo="deleteTodo"
    @desc="saveTodo"
    />
    <EditTodo v-if="state.edit"
    :editDescription="state.editDescription"
    :todoId="state.todoId"
    :cancelBtn="cancelBtn"
    @editTodo="editTodo"
    />
  </div>
</template>

<script>
import { reactive, computed } from '@vue/composition-api'
import Todo from '@/components/Todo.vue'
import EditTodo from '@/components/EditTodo.vue'

export default {
  name: 'todolist',
  components: {
    Todo,
    EditTodo
  },
  setup () {
    const state = reactive({
      description: '',
      editDescription: '',
      todoId: '',
      edit: false,
      todos: [
        {
          id: 1,
          description: 'Go to church',
          completed: false
        },
        {
          id: 2,
          description: 'Start my workout',
          completed: true
        }
      ],
      title: 'TodoList Application',
      setTodoId: computed(() => state.todos.length + 1)
    })

    function saveTodo (description) {
      const todo = {
        id: state.setTodoId,
        description: description,
        completed: false
      }
      state.description = ''
      state.todos.push(todo)
    }

    function deleteTodo (id) {
      state.todos = state.todos.filter((todo) => todo.id !== id)
    }

    function editBtn (id, description) {
      state.editDescription = description
      state.todoId = id
      state.edit = true
    }

    function cancelBtn () {
      state.edit = false
    }

    function editTodo (id, description) {
      state.todos = state.todos.map((todo) => {
        if (todo.id === Number(id)) {
          todo.description = description
        }
        return todo
      })
      state.edit = false
    }

    return {
      state,
      saveTodo,
      deleteTodo,
      editTodo,
      editBtn,
      cancelBtn
    }
  }
}
</script>

<style>

</style>
