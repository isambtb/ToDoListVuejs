<template>
  <div class="container my-5">
    <h2 class="text-center">VUE 3 ToDo App</h2>
    <div class="row d-flex justify-content-center">
      <todo-form v-on:add-todo="pushTodo" />
      <todo-list v-bind:todos="todos" />
    </div>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import TodoForm from "../components/TodoForm.vue";
import TodoList from "../components/TodoList.vue";

@Options({
  components: {
    TodoForm,
    TodoList,
  },
  data() {
    return {
      todos: Array,
    };
  },
  methods: {
    async getTodos() {
      this.todos = [
        {
          id: 1,
          todo: "Wake up!",
          done: false,
        },
        {
          id: 2,
          todo: "Go to bed!",
          done: false,
        },
      ];
    },
    async pushTodo(todo: any) {
      this.todos.push(todo);
    },
  },
  async mounted() {
    await this.getTodos();
  },
})
export default class Main extends Vue {}
</script>
