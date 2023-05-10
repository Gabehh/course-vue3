<template>
  <form class="add-todo-form">
    <input type="text" v-model="todoTittle" placeholder="Todo Title" />
    <div>
      <button @click.prevent="$emit('submit', todoTittle)">Add Todo</button>
    </div>
  </form>
</template>

<script>
export default{
    data (){
        return {
            todoTittle: "",
        };
    },
    emits: ['submit']
}
</script>

<style>
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