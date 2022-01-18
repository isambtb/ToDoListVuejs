<template>
  <div class="row d-flex justify-content-center mt-3" v-if="todos.length">
    <div class="col-md-6">
      <h5 class="mb-3">Todo List</h5>
      <div style="list-style-type: none">
        <ul>
          <li
            v-for="(todo, index) in todos"
            :key="index"
            class="row"
            style="
              display: flex;
              justify-content: space-between;
              align-items: center;
              padding: 10px 24px;
              border-radius: 6px;
              margin-bottom: 12px;
              border: 2px solid hsla(0, 0%, 0%, 0.35);
            "
          >
            <div class="col-8">
              <span
                v-bind:style="todo.done ? 'text-decoration:line-through;' : ''"
                >{{ todo.todo }}</span
              >
            </div>
            <div class="col-2 d-flex justify-content-center">
              <span
                class="form-check form-switch"
                @click="setTodoToDone(todo)"
                style="margin-left: 20px"
              >
                <input
                  class="form-check-input"
                  type="checkbox"
                  role="switch"
                  id="flexSwitchCheckDefault"
                  data-onstyle="#1f2023"
                  :checked="todo.done"
                />
              </span>
            </div>
            <div class="col-2 d-flex justify-content-center">
              <button class="btn btn-danger btn-sm" @click="deleteTodo(index)">
                Delete
              </button>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted } from "vue";

interface IValue {
  id: string;
  todo: string;
  done: boolean;
}

export default defineComponent({
  name: "TodoList",
  props: {
    todos: Array,
  },
  methods: {
    async deleteTodo(index: number) {
      this.todos?.splice(index, 1);
    },
    async setTodoToDone(todo: IValue) {
      todo.done = !todo.done;
    },
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="sass">
</style>