<template>
  <Navbar/>
  <main class="container">
    <Alert
      message="Todo title is required"
      :show="showAlert"
      @close="showAlert = false"
      type="info"
    />
    <section>
      <AddTodoForm @submit="addTodo"/>
    </section>
    <section>
      <Todo
        v-for="todo in todos"
        :key="todo.id"
        :title="todo.title"
        @remove="removeTodo(todo.id)"
      />
    </section>
  </main>
</template>

<script>
import AddTodoForm from "./components/AddTodoForm.vue";
import Alert from "./components/Alert.vue";
import Navbar from "./components/Navbar.vue";
import Todo from "./components/Todo.vue";

export default {
  components: {
    Alert,
    Navbar,
    AddTodoForm,
    Todo
},
  data() {
    return {
      todoTittle: "",
      todos: [],
      showAlert: false,
    };
  },
  methods: {
    addTodo(title) {
      if (title === "") {
        this.showAlert = true;
        return;
      } else this.showAlert = false;
      //e.preventDefault(); // Para que no refresque la página (ya que intenta mandarlo a un servidor porque el botón está dentro del formulario)
      this.todos.push({
        title,
        id: Math.floor(Math.random() * 1000),
      });
    },
    removeTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id); // Se crea una lista nueva y se asigna a la que ya estaba antes
    },
  },
};
</script>

<style scoped>
.alert {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: var(--danger-color);
  margin-bottom: 20px;
  padding: 0 20px 0 20px;
  border-radius: 10px;
  height: 50px;
}

.close-alert {
  font-size: 50px;
  cursor: pointer;
}

</style>
