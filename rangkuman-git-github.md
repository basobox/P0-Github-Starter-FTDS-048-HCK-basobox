# Rangkuman Lengkap Git & GitHub

Panduan praktis penggunaan **Git** (sistem kontrol versi lokal) dan **GitHub** (platform hosting repositori cloud), termasuk pengaturan **SSH Key** dan alur kerja (*workflow*) harian.

---

## 1. Konsep Dasar: Git vs GitHub

| Aspek | Git | GitHub |
| :--- | :--- | :--- |
| **Definisi** | *Version Control System* (VCS) untuk melacak perubahan kode. | Layanan *cloud* untuk menyimpan dan berkolaborasi pada repositori Git. |
| **Lokasi** | Berjalan secara **lokal** di komputer/laptop pengguna. | Berjalan secara **online** di server internet. |
| **Fungsi Utama** | Mencatat riwayat revisi, membuat *branch*, dan mengembalikan versi kode. | Backup kode, kolaborasi tim (*Pull Request*), dan manajemen proyek. |

---

## 2. Konfigurasi Awal Git (Wajib Dilakukan Sekali)

Sebelum mulai bekerja, atur identitas lokal agar setiap perubahan (*commit*) tercatat atas nama kamu:

```bash
git config --global user.name "basobox"
git config --global user.email "nawafi.suren@gmail.com"
```

Cek konfigurasi yang sudah tersimpan:
```bash
git config --list
```

---

## 3. Autentikasi ke GitHub (Menggunakan SSH)

GitHub sudah tidak mendukung penggunaan *password* akun biasa untuk operasi Git melalui terminal. Metode paling aman dan praktis adalah menggunakan **SSH Key**.

### Langkah Setup SSH Key (Linux / macOS / WSL)
1. **Buat pasangan SSH Key baru:**
   ```bash
   ssh-keygen -t ed25519 -C "email_github_kamu@example.com"
   ```
   *(Tekan **Enter** pada semua pertanyaan untuk menggunakan lokasi default dan tanpa passphrase).*

2. **Jalankan SSH Agent dan daftarkan private key:**
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   ```

3. **Tampilkan dan salin Public Key:**
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```
   *(Salin seluruh output yang diawali dengan `ssh-ed25519 ...`).*

4. **Tambahkan ke Akun GitHub:**
   - Buka **GitHub** > **Settings** > **SSH and GPG keys** > **New SSH key**.
   - Tempel (*paste*) kode kunci ke kolom **Key** dan simpan.

5. **Uji koneksi SSH:**
   ```bash
   ssh -T git@github.com
   ```
   *(Jika berhasil, akan muncul pesan: `Hi <username>! You've successfully authenticated...`).*

---

## 4. Alur Kerja Dasar (Workflow Harian)

Secara garis besar, file di dalam proyek Git melewati tiga area utama:
`Working Directory` ➔ *(git add)* ➔ `Staging Area` ➔ *(git commit)* ➔ `Local Repository` ➔ *(git push)* ➔ `GitHub (Remote)`

### A. Memulai Proyek
* **Mengunduh repositori yang sudah ada di GitHub (Clone):**
  ```bash
  git clone git@github.com:username/nama-repo.git
  ```
* **Membuat repositori baru dari folder lokal:**
  ```bash
  git init
  git branch -M main
  git remote add origin git@github.com:username/nama-repo.git
  ```

### B. Menyimpan & Mengirim Perubahan
1. **Cek status file yang diubah/ditambahkan:**
   ```bash
   git status
   ```
2. **Masukkan file ke Staging Area:**
   ```bash
   git add nama_file.py   # Menambah satu file spesifik
   git add .              # Menambah semua file yang berubah
   ```
3. **Simpan perubahan ke riwayat lokal (Commit):**
   ```bash
   git commit -m "Pesan singkat yang menjelaskan perubahan"
   ```
4. **Kirim perubahan ke GitHub (Push):**
   ```bash
   git push origin main
   ```

### C. Mengambil Pembaruan dari GitHub
* **Mengunduh dan menggabungkan perubahan terbaru dari remote:**
  ```bash
  git pull origin main
  ```

---

## 5. Manajemen Branch (Percabangan)

*Branch* digunakan untuk mengerjakan fitur baru atau eksperimen tanpa mengganggu kode utama (`main`).

| Perintah | Fungsi |
| :--- | :--- |
| `git branch` | Melihat daftar semua *branch* lokal (`*` menandakan posisi aktif). |
| `git branch nama-branch` | Membuat *branch* baru. |
| `git checkout nama-branch` | Pindah ke *branch* tertentu. |
| `git checkout -b nama-branch` | Membuat sekaligus langsung pindah ke *branch* baru. |
| `git merge nama-branch` | Menggabungkan perubahan dari `nama-branch` ke *branch* yang sedang aktif. |
| `git branch -d nama-branch` | Menghapus *branch* lokal yang sudah selesai digabungkan. |

---

## 6. Perintah Penting Lainnya (Riwayat & Pembatalan)

* **Melihat riwayat commit:**
  ```bash
  git log --oneline
  ```
* **Melihat daftar koneksi remote repository:**
  ```bash
  git remote -v
  ```
* **Membatalkan perubahan pada file sebelum `git add`:**
  ```bash
  git checkout -- nama_file.py
  ```
* **Mengeluarkan file dari Staging Area (batal `git add`):**
  ```bash
  git reset HEAD nama_file.py
  ```
* **Mengubah pesan commit terakhir (sebelum di-push):**
  ```bash
  git commit --amend -m "Pesan commit baru yang diperbaiki"
  ```

---

## 7. Tips & Praktik Terbaik

1. **Gunakan file `.gitignore`:** Buat file bernama `.gitignore` di folder utama proyek untuk mengecualikan file sensitif atau tidak perlu (seperti `.env`, `node_modules/`, `__pycache__/`, `.DS_Store`) agar tidak ikut terunggah ke GitHub.
2. **Tulis pesan commit yang jelas:** Gunakan kata kerja aktif yang deskriptif (contoh: `"Menambahkan fungsi pembersihan data"` daripada `"update"`).
3. **Selalu `git pull` sebelum mulai bekerja:** Jika berkolaborasi dalam tim, pastikan repositori lokal selalu dalam kondisi terbaru untuk menghindari konflik kode (*merge conflict*).    





reff: nawafi.suren@gmail.com | https://share.google/aimode/GI3SMKYw2jtRnJUTW