# Rick & Morty Character Explorer

Aplikasi mobile Flutter untuk latihan responsi praktikum pemrograman mobile. Aplikasi ini menampilkan daftar karakter, detail karakter, filter status, daftar episode, serta sistem manajemen favorit dan autentikasi pengguna.

---

## 🛠️ Tech Stack & Library
- **State Management & Routing**: [GetX](https://pub.dev/packages/get) (`^4.6.6`)
- **Local Database (Auth/User Registry)**: [Hive](https://pub.dev/packages/hive) & [hive_flutter](https://pub.dev/packages/hive_flutter) (`^2.2.3`)
- **Session & Favorite Persistence**: [shared_preferences](https://pub.dev/packages/shared_preferences) (`^2.2.2`)
- **REST API Client**: [http](https://pub.dev/packages/http) (`^1.2.0`)
- **Design System**: Material 3 dengan custom dark Rick & Morty portal theme

---

## 📌 Kesesuaian Soal Latihan Responsi

| No | Fitur / Kebutuhan | Status | Implementasi |
|---|---|:---:|---|
| **1** | **Login & Register** (Local DB & Shared Preferences) | ✅ | Register menyimpan user ke **Hive** (`UserModel`). Login memvalidasi ke Hive dan menyimpan session aktif ke **SharedPreferences** (`is_logged_in`). Dilengkapi tombol logout di AppBar. |
| **2a** | **Home Screen: Daftar Karakter** | ✅ | Menampilkan foto/avatar, nama, dan status karakter dari API Rick & Morty dengan tombol toggle favorit di setiap kartu. |
| **2b** | **Filter Status Karakter** | ✅ | Filter chip untuk status: `All`, `Alive`, `Dead`, dan `Unknown` (`/character?status=...`). |
| **2c** | **Navigasi ke Detail Screen** | ✅ | Ketuk pada kartu karakter untuk membuka `CharacterDetailView`. |
| **3a** | **Detail Screen: Info Lengkap** | ✅ | Menampilkan foto hero, nama, status badge, spesies, gender, origin (asal), dan location. |
| **3b-d** | **Detail Screen: Tombol Favorit & SnackBar** | ✅ | Tombol favorit dinamis (icon hati terisi/kosong). Menampilkan SnackBar saat ditambahkan/dihapus dari favorit. |
| **4a** | **Favorite Screen: Simpan dengan SharedPreferences** | ✅ | Data favorit disimpan persisten dalam bentuk JSON di `SharedPreferences`. |
| **4b** | **Favorite Screen: Hapus dengan Swipe** | ✅ | Menggunakan widget `Dismissible` dengan aksi geser dari kanan ke kiri untuk menghapus. |
| **4c** | **Favorite Screen: SnackBar saat Dihapus** | ✅ | Menampilkan `Get.snackbar` setelah karakter berhasil dihapus via swipe. |
| **4d** | **Favorite Screen: Empty State** | ✅ | Menampilkan pesan `"Daftar favorite masih kosong"` jika belum ada favorit. |
| **5** | **Halaman Episode** | ✅ | Menampilkan list episode dari API (`/episode`) berisi nama episode dan `air_date` serta kode episode. |
| **6a** | **Bottom Navigation Bar** | ✅ | Berpindah antar 3 tab: `Characters`, `Favorites`, dan `Episodes`. |
| **6b** | **Loading & Error Handling** | ✅ | Indikator loading (`CircularProgressIndicator`) dan tampilan error dengan tombol retry jika API gagal diakses. |
| **6c** | **Sinkronisasi Reaktif Favorit** | ✅ | Menggunakan GetX reaktif (`RxList<CharacterModel> favorites`), status favorit otomatis tersinkronisasi instan di Home, Detail, dan Favorite Screen. |
| **6d** | **Proteksi Halaman Utama** | ✅ | Auto-check session di `main.dart`. Jika belum login diarahkan ke `LoginView`, jika sudah login langsung ke `MainNavView`. |
| **Bonus 1** | **Pencarian Karakter by Name** | ✅ | Search bar pencarian karakter berdasarkan nama pada Home Screen (`/character/?name=...`). |
| **Bonus 2** | **Desain UI Menarik & Konsisten** | ✅ | Desain modern Rick & Morty dark theme dengan aksen hijau portal neon (`#00E599`) dan sci-fi cyan. |

---

## 📁 Struktur Folder
```text
lib/
├── controllers/
│   ├── auth_controller.dart        # Logika login, register, logout, session
│   ├── character_controller.dart   # Fetch API karakter, filter status, search
│   ├── episode_controller.dart     # Fetch API list episode
│   └── favorite_controller.dart    # Reaktif list favorit, swipe delete, snackbar
├── models/
│   ├── character_model.dart        # Serialisasi JSON karakter Rick & Morty
│   ├── episode_model.dart          # Serialisasi JSON episode
│   └── user_model.dart            # Model & Hive TypeAdapter pengguna
├── services/
│   ├── api_service.dart            # HTTP Client ke rickandmortyapi.com
│   ├── auth_service.dart           # Hive database & session SharedPreferences
│   └── favorite_service.dart       # Penyimpanan daftar favorit di SharedPreferences
├── utils/
│   └── app_theme.dart              # Rick & Morty custom palette & typography
├── views/
│   ├── auth/
│   │   ├── login_view.dart         # Halaman login
│   │   └── register_view.dart      # Halaman register akun
│   ├── detail/
│   │   └── character_detail_view.dart # Halaman detail karakter lengkap
│   └── home/
│       ├── character_list_view.dart   # Tab 1: Daftar karakter, search & filter
│       ├── episode_list_view.dart     # Tab 3: Daftar episode
│       ├── favorite_list_view.dart    # Tab 2: Daftar favorit dengan swipe
│       └── main_nav_view.dart         # Bottom Navigation Bar & Logout dialog
└── main.dart                       # Inisialisasi Hive, session check & GetMaterialApp
```

---

## 🚀 Cara Menjalankan Aplikasi
1. Buka terminal di folder project ini (`d:\semester 5\Prak Mobile\latihan responsi`).
2. Pastikan emulator Android, iOS Simulator, Chrome, atau Windows desktop device tersedia:
   ```bash
   flutter run
   ```
3. Registrasi akun baru di aplikasi, lalu masuk dengan username dan password yang telah didaftarkan.

