# Panduan Memindahkan & Push Repositori ke Akun GitHub Pribadi

Panduan ini menjelaskan cara mengunggah (*push*) kode dari repositori tugas (`FTDS-Assignment-Bay-2`) ke repositori milikmu sendiri (`basobox`) menggunakan SSH.

---

## Langkah 1: Buat Repositori Kosong di Akun GitHub Pribadi

1. Buka profil GitHub kamu (`https://github.com/basobox`), lalu klik tab **Repositories** (atau ikon **`+`** di pojok kanan atas) > pilih **New**.
2. Isi **Repository name** dengan:
   ```text
   P0-Github-Starter-FTDS-048-HCK-basobox
   ```
3. Pilih visibilitas repositori (**Public** atau **Private**) sesuai kebutuhan.
4. **Penting:** Biarkan opsi *Add a README file*, *.gitignore*, dan *License* dalam keadaan **kosong (tidak dicentang)** agar tidak terjadi konflik riwayat *commit*.
5. Klik **Create repository**.

---

## Langkah 2: Arahkan Remote & Push dari Terminal

Pastikan posisi terminal kamu berada di dalam direktori proyek (`~/P0-Github-Starter-FTDS-048-HCK-basobox`), lalu pilih salah satu dari dua opsi berikut:

### Opsi A: Menyimpan ke Kedua Repositori (Disarankan untuk Tugas)
Gunakan cara ini jika kamu tetap ingin mengirim tugas ke repositori utama (`origin`) sekaligus menyimpan salinan di akun pribadimu (`personal`).

1. **Tambahkan remote baru bernama `personal`:**
   ```bash
   git remote add personal git@github.com:basobox/P0-Github-Starter-FTDS-048-HCK-basobox.git
   ```
2. **Push kode ke repositori pribadi:**
   ```bash
   git push -u personal main
   ```
3. **Cara penggunaan selanjutnya:**
   * Untuk mengirim update ke **repositori tugas utama**:
     ```bash
     git push origin main
     ```
   * Untuk menyimpan salinan ke **repositori pribadi**:
     ```bash
     git push personal main
     ```

---

### Opsi B: Mengganti Tujuan Sepenuhnya ke Akun Pribadi
Gunakan cara ini jika kamu ingin memindahkan alamat utama (`origin`) sepenuhnya ke akun `basobox`.

1. **Ubah URL `origin` ke repositori pribadimu:**
   ```bash
   git remote set-url origin git@github.com:basobox/P0-Github-Starter-FTDS-048-HCK-basobox.git
   ```
2. **Verifikasi perubahan alamat remote:**
   ```bash
   git remote -v
   ```
   *(Pastikan URL yang tampil sudah mengarah ke `git@github.com:basobox/P0-Github-Starter-FTDS-048-HCK-basobox.git`)*.
3. **Push kode ke repositori pribadi:**
   ```bash
   git push -u origin main
   ```
