# ⚙️ Backend - Laravel Todo API

REST API untuk aplikasi Todo menggunakan Laravel

---

## 🚀 Tech Stack

* Laravel 10+
* MySQL

---

## ⚙️ Installation

```bash
composer install
cp .env.example .env
```

---

## 🗄️ Setup Database

Edit `.env`:

```
DB_DATABASE=backend-api
DB_USERNAME=root
DB_PASSWORD=
```

---

## ▶️ Run Migration

```bash
php artisan migrate
```

---

## ▶️ Jalankan Server

```bash
php artisan serve
```

---

### Todo

| Method | Endpoint        |
| ------ | --------------- |
| GET    | /api/todos      |
| POST   | /api/todos      |
| PUT    | /api/todos/{id} |
| DELETE | /api/todos/{id} |

---

## 📁 Struktur

```
app/
├── Models/
├── Http/
│   ├── Controllers/
│   │   ├── TodoController.php
```

---

## 💡 Notes

Gunakan Postman / frontend Vue untuk testing API.
