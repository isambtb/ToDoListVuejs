<template>
  <div class="col-xs-12 col-lg-6 my-3">
    <div class="form-group mb-3">
      <label for="todo" class="form-label">Add ToDo</label>
      <div class="row">
        <div class="col-10">
          <input
            type="text"
            class="form-control"
            id="todo"
            v-model="todo"
            placeholder="Add new todo"
            name="todo"
            v-bind:class="{
              'is-invalid': input_errors.length > 0,
              'is-valid': input_errors.length == 0 && todo != '',
            }"
            required
          />
        </div>
        <div class="invalid-feedback">
          <span v-for="(error, index) in input_errors" :key="index">{{
            error
          }}</span>
        </div>

        <div class="col-2 d-grid gap-2">
          <input
            class="btn btn-primary btn-s float-end"
            type="submit"
            valut="submit"
            @click="addNewValue"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

interface IValue {
  todo: string;
  checkForm: boolean;
  input_errors: string[];
}

export default defineComponent({
  name: "TodoForm",
  components: {},
  data(): IValue {
    return {
      todo: "",
      checkForm: false,
      input_errors: [],
    };
  },
  methods: {
    async generateId(): Promise<string> {
      return "_" + Math.random().toString(36).substr(2, 9);
    },
    addNewValue(): void {
      const newTodo = {
        id: this.generateId(),
        todo: this.todo,
        done: false,
      };
      this.todo = "";
      if (newTodo.todo !== "") {
        this.$emit("add-todo", newTodo);
      }
    },
  },
  watch: {
    todo(val) {
      this.input_errors = [];
      if (val === "") {
        this.input_errors.push("ToDo field cannot be left blank");
        return;
      }
      if (val.length < 3 || val.length > 40) {
        this.input_errors.push(
          "ToDo field be Minimum 6, Maximum 25 characters"
        );
        return;
      }
    },
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="sass">
</style>