<template>
  <div>
    <p
      class="tasks"
    >Completed Tasks: {{todos.filter(todo => {return todo.done === true}).length}} Pending Tasks: {{todos.filter(todo => {return todo.done === false}).length}}</p>
    <todo
      v-on:delete-todo="deleteTodo"
      v-on:complete-todo="completeTodo"
      v-for="todo in todos"
      :todo.sync="todo"
      v-bind:key="todo"
    ></todo>
  </div>
</template>

<script type = "text/javascript" >
import swal from "sweetalert2";
import Todo from "./Todo";

export default {
  props: ["todos"],
  components: {
    Todo
  },
  methods: {
    deleteTodo(todo) {
      swal.fire({
        icon: "warning",
        title: "Are you sure ?",
        text: "You will not be able to recover this page !",
        showCancelButton: true,
        confirmButtonColor: "#ff0000",
        confirmButtonText: "Yes, delete it !",
        cancelButtonText: "No, cancel !",
        preConfirm: () => {
          const todoIndex = this.todos.indexOf(todo);
          this.todos.splice(todoIndex, 1);
          swal.fire("Deleted!", "Your To-Do has been deleted.", "success");
        }
      });
    },
    completeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos[todoIndex].done = true;
      swal.fire("Success!", "To-Do completed!", "success");
    }
  }
};
</script>

<style scoped>
p.tasks {
  text-align: center;
}
</style>
