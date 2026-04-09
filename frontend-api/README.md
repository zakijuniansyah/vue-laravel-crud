# 🎨 Vue Todo App (Frontend)

Frontend aplikasi Todo modern menggunakan **Vue 3 + Composition API** dengan tampilan **dark mode elegan** dan dukungan **offline (fallback mode)**.

---

## 🚀 Tech Stack

* ⚡ Vue 3 (Composition API)
* 🔗 Axios
* 🎨 Tailwind CSS (Modern UI)
* 🌙 Dark Mode UI

---

## ⚙️ Installation

Clone project lalu jalankan:

```bash
npm install
npm run dev
```

Aplikasi akan berjalan di:

```
http://localhost:5173
```

---

## 🔗 Koneksi API

Edit file berikut:

```
src/services/api.js
```

Lalu sesuaikan `baseURL`:

```js
baseURL: "http://127.0.0.1:8000/api"
```

---

## 📁 Struktur Folder

```
src/
├── views/
│   └── Dashboard.vue     # Halaman utama Todo
│
├── services/
│   └── api.js            # Konfigurasi Axios
```

---

## 🎨 UI Features

* 🌙 Dark Mode modern (default)
* 💎 Clean & professional design (Tailwind CSS)
* ⚡ Smooth interaction & transition
* 📱 Responsive (mobile friendly)

---

## 📌 Fitur Utama

* ✅ CRUD Todo (Create, Read, Update, Delete)
* 🔄 Toggle status (completed / not completed)
* ❌ Delete dengan konfirmasi
* ⚠️ Error handling (anti blank screen)
* 📴 Offline fallback mode (tetap bisa digunakan tanpa API)

---

## 💡 Notes

* Backend menggunakan Laravel API
* Pastikan backend berjalan di:

```
http://127.0.0.1:8000
```

---

## 🔥 Mode Offline (Fallback)

Jika API tidak aktif:

* Data dummy otomatis ditampilkan
* User tetap bisa:

  * ➕ Menambah todo
  * ✔️ Toggle status
  * 🗑️ Menghapus todo

---

## 📸 Preview

UI menggunakan:

* Dark theme
* Card layout
* Modern input & button

---

## 🚀 Future Improvements

* 🔍 Search & filter todo
* 🏷️ Kategori todo
* 💾 LocalStorage persistence
* 🌗 Toggle Dark / Light Mode
* 🔔 Notifikasi

---

## 👨‍💻 Author

**Zaki Juniansyah**
Frontend Developer (Vue & Laravel Enthusiast)

---

## ⭐ Support

Jika project ini membantu, jangan lupa ⭐ di GitHub ya!
