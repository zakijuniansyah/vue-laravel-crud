<script setup>
import { onMounted, ref } from 'vue';
import api from '../services/api';

const todos = ref([]);
const loading = ref(false);
const error = ref(null);

// input state
const title = ref("");
const submitting = ref(false);

// GET DATA
const getTodos = async () => {
  loading.value = true;
  error.value = null;

  try {
    const res = await api.get("/todos");
    todos.value = res.data?.data || res.data || [];
  } catch (err) {
    console.log("API ERROR:", err);

    // 🔥 fallback data
    todos.value = [
      { id: 1, title: "Belajar Vue + Laravel", completed: false },
      { id: 2, title: "Bikin Todo App keren", completed: true },
    ];

    error.value = "API tidak aktif (mode demo)";
  } finally {
    loading.value = false;
  }
};

// ADD TODO
const addTodo = async () => {
  if (!title.value) return;

  submitting.value = true;

  try {
    await api.post("/todos", {
      title: title.value,
      completed: false
    });

    getTodos();
  } catch (err) {
    // 🔥 fallback local
    todos.value.push({
      id: Date.now(),
      title: title.value,
      completed: false
    });
  } finally {
    title.value = "";
    submitting.value = false;
  }
};

// TOGGLE TODO
const toggleTodo = async (todo) => {
  try {
    await api.put(`/todos/${todo.id}`, {
      title: todo.title,
      completed: !todo.completed
    });

    getTodos();
  } catch (err) {
    // 🔥 fallback local
    todo.completed = !todo.completed;
  }
};

// DELETE TODO
const deleteTodo = async (id) => {
  const confirmDelete = confirm('Yakin mau dihapus?');
  if (!confirmDelete) return;

  try {
    await api.delete(`/todos/${id}`);
    getTodos();
  } catch (err) {
    // 🔥 fallback local
    todos.value = todos.value.filter(t => t.id !== id);
  }
};

// MOUNT
onMounted(() => {
  getTodos();
});
</script>


<template>
  <div class="min-h-screen bg-gray-900 flex items-center justify-center p-6">
    <div class="w-full max-w-xl bg-gray-800 shadow-2xl rounded-2xl p-6">

      <!-- TITLE -->
      <h1 class="text-2xl font-bold text-white mb-6 text-center">
        📝 Todo App
      </h1>

      <!-- FORM -->
      <form @submit.prevent="addTodo" class="flex gap-2 mb-4">
        <input
          v-model="title"
          placeholder="Masukkan todo..."
          class="flex-1 px-4 py-2 bg-gray-700 text-white border border-gray-600 rounded-xl focus:outline-none focus:ring-2 focus:ring-blue-500 placeholder-gray-400"
        />
        <button
          type="submit"
          class="px-4 py-2 bg-blue-600 text-white rounded-xl hover:bg-blue-700 transition disabled:opacity-50"
          :disabled="submitting"
        >
          {{ submitting ? "..." : "+" }}
        </button>
      </form>

      <!-- STATE -->
      <p v-if="loading" class="text-gray-400 text-center">Loading...</p>

      <p v-if="error" class="text-yellow-400 text-center mb-2">
        {{ error }}
      </p>

      <p v-if="!loading && todos && todos.length === 0" class="text-gray-500 text-center">
        Belum ada todo 😢
      </p>

      <!-- LIST -->
      <ul class="space-y-3 mt-4">
        <li
          v-for="todo in todos"
          :key="todo.id"
          class="flex items-center justify-between bg-gray-700 p-3 rounded-xl shadow-md hover:bg-gray-600 transition"
        >
          <!-- LEFT -->
          <div class="flex items-center gap-3">
            <input
              type="checkbox"
              :checked="todo.completed"
              @change="toggleTodo(todo)"
              class="w-5 h-5 accent-blue-500 cursor-pointer"
            />

            <span
              class="text-gray-100"
              :class="{
                'line-through text-gray-400': todo.completed
              }"
            >
              {{ todo.title }}
            </span>
          </div>

          <!-- DELETE -->
          <button
            @click="deleteTodo(todo.id)"
            class="text-red-400 hover:text-red-600 transition text-lg"
          >
            🗑️
          </button>
        </li>
      </ul>

    </div>
  </div>
</template>