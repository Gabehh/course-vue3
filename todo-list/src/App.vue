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
      <div v-for="todo in todos" class="todo" :key="todo.id">
        <p>{{ todo.title }}</p>
        <div>
          <button @click="removeTodo(todo)" class="remove-todo-btn">
            &times;
          </button>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import AddTodoForm from "./components/AddTodoForm.vue";
import Alert from "./components/Alert.vue";
import Navbar from "./components/Navbar.vue";
export default {
  components: {
    Alert,
    Navbar,
    AddTodoForm
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
    removeTodo(todoTittle) {
      this.todos = this.todos.filter((x) => x !== todoTittle); // Se crea una lista nueva y se asigna a la que ya estaba antes
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
