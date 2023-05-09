<template>
  <nav class="navbar">
    <img src="./assets/logo.svg" width="50" />
    <div class="brand">Todo List App</div>
  </nav>

  <main class="container">
    <div v-if="showAlert" class="alert">
      <div>Todo title is required</div>
      <div @click="showAlert = false" class="close-alert">&times;</div>
    </div>
    <section>
      <form class="add-todo-form">
        <input type="text" v-model="todoTittle" placeholder="Todo Title" />
        <div>
          <button @click.prevent="addTodo">Add Todo</button> 
        </div>
      </form>
    </section>
    <section>
      <div v-for="(todo) in todos" class="todo" :key="todo.id">
        <p>{{ todo.title }}</p>
        <div>
          <button @click="removeTodo(todo)" class="remove-todo-btn">&times;</button>
        </div>
      </div>
    </section>
  </main>

</template>

<script>
  export default {
    data(){
      return  {
        todoTittle: "",
        todos: [],
        showAlert: false
      }
    },
    methods:{
      addTodo(){
        if(this.todoTittle === ""){
          this.showAlert = true;
          return;
        }
        else
          this.showAlert = false
        //e.preventDefault(); // Para que no refresque la página (ya que intenta mandarlo a un servidor porque el botón está dentro del formulario)
        this.todos.push({
          title: this.todoTittle,
          id: Math.floor(Math.random()*1000)
        });
      },
      removeTodo(todoTittle){
        this.todos = this.todos.filter(x=> x !== todoTittle) // Se crea una lista nueva y se asigna a la que ya estaba antes
      }
    }
  };
</script>

<style scoped>
.navbar {
  display: flex;
  align-items: center;
  background: var(--navbar-color);
  padding: 20px;
  margin-bottom: 30px;
}
.brand {
  font-size: 2rem;
}

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

.close-alert{
  font-size:50px;
  cursor: pointer;
}
.add-todo-form {
  display: flex;
  justify-content: space-between;
}
.add-todo-form input {
  width: 80%;
  border: solid 2px var(--accent-color);
}
.add-todo-form button {
  background: var(--accent-color);
  color: var(--text-color);
  border: none;
  height: 50px;
}

.todo {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: var(--accent-color);
  margin-top: 30px;
  padding: 0 20px 0 20px;
  border-radius: 10px;
}

.remove-todo-btn {
  border-radius: 50%;
  border: none;
  height: 40px;
  width: 40px;
  font-size: 30px;
  color: var(--text-color);
  background: var(--danger-color);
  cursor: pointer;
}
</style>
