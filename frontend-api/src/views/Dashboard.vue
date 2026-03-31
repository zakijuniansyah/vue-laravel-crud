<script setup>
import { onMounted, ref } from 'vue';
import api from '../services/api';

const todos = ref([]);
const loading = ref(false);
const error = ref(null);

// state untuk input
const title = ref("");
const submitting = ref(false);

// get data
const getTodos = async () => {
  loading.value = true;
  try {
    const res = await api.get("/todos");
    todos.value = res.data.data;
  } catch (error) {
    error.value = "gagal mengambil data"
  } finally {
    loading.value = false;
  }
}

// post data
const addTodo = async () => {
  if(!title.value) return;

  submitting.value = true;
  try {
    await api.post("/todos", {
      title: title.value,
      completed: false
    });

    title.value = ("");
    getTodos();
  } catch (error) {
    error.value = 'gagal menambah data'
  } finally {
    submitting.value = false
  }
}

// update data
const toggleTodo = async (todo) => {
  try {
    await api.put(`/todos/${todo.id}`, {
      title: todo.title,
      completed: !todo.completed
    });

    getTodos();
  } catch (error) {
    error.value = "gagal update data";
  }
}

// delete
const deleteTodo = async (id) => {
  const confirmDelete = confirm('Yakin mau dihapus?');

  if(!confirmDelete) return;
  
  try {
    await api.delete(`/todos/${id}`);
    getTodos();
  } catch (error) {
    error.value = 'gagal menghapus data';
  }
}

onMounted(() => {
  getTodos();
})
</script>

<template>
  <div class="container">
  <h1 class="title">📝 Todo App</h1>

  <!-- FORM -->
  <form @submit.prevent="addTodo" class="form">
    <input v-model="title" placeholder="Masukan Todo..." class="input" />
    <button type="submit" class="btn">
      {{ submitting ? "..." : "+" }}
    </button>
  </form>

  <!-- STATE -->
  <p v-if="loading" class="loading">Loading...</p>
  <p v-if="error" class="error">{{ error }}</p>
  <p v-if="todos.length === 0" class="empty">Belum ada todo 😢</p>

  <!-- LIST -->
  <ul class="list">
    <li v-for="todo in todos" :key="todo.id" class="todo-item">
      
      <div class="todo-left">
        <input
          type="checkbox"
          :checked="todo.completed"
          @change="toggleTodo(todo)"
        />

        <span
          class="todo-text"
          :class="{ completed: todo.completed }"
        >
          {{ todo.title }}
        </span>
      </div>

      <button class="delete-btn" @click="deleteTodo(todo.id)">
        🗑️
      </button>

    </li>
  </ul>
</div>
</template>