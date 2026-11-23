# Panduan Alur Kerja (Workflow) Git Anti-Bentrok & Penyelesaian Konflik

Dokumen ini berisi standar alur kerja harian (*best practice*) untuk menjaga repositori tetap sinkron saat sedang dalam proses pengerjaan (*in progress*), serta langkah darurat jika terjadi bentrok (*merge conflict*).

---

## 1. Siklus Harian (Untuk Kerja Mandiri / Tugas Individu)

Gunakan alur ini jika kamu mengerjakan repositori sendirian (misalnya berpindah antar perangkat atau sesekali melakukan perubahan kecil di GitHub):

```text
[Buka VS Code] ──▶ git pull ──▶ [Edit Kode] ──▶ git add & commit ──▶ git push ──▶ [Tutup VS Code]
```

### Langkah-Langkah Eksekusi:
1. **Sebelum Mengetik Kode (Wajib):**
   Selalu tarik versi paling baru dari GitHub agar folder lokal sejajar dengan *cloud*.
   ```bash
   git pull origin main
   ```
2. **Saat Mengerjakan Tugas:**
   Lakukan *commit* secara berkala setiap kali menyelesaikan satu bagian kecil (hindari menumpuk terlalu banyak perubahan dalam satu *commit*).
   ```bash
   git add .
   git commit -m "Menambahkan fungsi pembersihan data"
   ```
3. **Sebelum Menutup VS Code / Berhenti:**
   Segera unggah (*push*) hasil kerja ke GitHub agar progres tersimpan aman.
   ```bash
   git push origin main
   ```

---

## 2. Alur *Feature Branch* (Paling Aman untuk Repo Sedang Progress)

Jika repositori sedang dikerjakan oleh tim atau kamu sedang menguji fitur yang belum matang, **jangan bekerja langsung di *branch* `main`**. Pisahkan pekerjaan ke dalam *branch* baru.

```text
main (Stabil) ──┬──▶ buat branch baru (fitur-x) ──▶ [Kerjakan & Commit] ──▶ push branch ──▶ Pull Request / Merge
                │
                └──▶ (Tetap bersih dari kode setengah jadi)
```

### Langkah-Langkah Eksekusi:
1. **Pastikan *Branch* `main` Lokal Paling Update:**
   ```bash
   git checkout main
   git pull origin main
   ```
2. **Buat & Pindah ke *Branch* Baru:**
   ```bash
   git checkout -b fitur-eda
   ```
3. **Kerjakan, *Commit*, dan *Push* ke *Branch* Tersebut:**
   ```bash
   git add .
   git commit -m "Selesai eksplorasi data awal"
   git push -u origin fitur-eda
   ```
4. **Gabungkan (*Merge*) Saat Sudah Selesai:**
   * **Jika bekerja dalam tim:** Buka GitHub dan buat **Pull Request (PR)** dari `fitur-eda` ke `main` untuk direview.
   * **Jika kerja mandiri di lokal:**
     ```bash
     git checkout main
     git pull origin main
     git merge fitur-eda
     git push origin main
     ```

---

## 3. Tiga Aturan Emas Anti-Bentrok

1. **Hindari Edit Langsung di Web GitHub:** Jangan mengedit file melalui browser GitHub jika kamu juga sedang membukanya di VS Code. Pusatkan semua pengeditan dari VS Code.
2. **Satu File, Satu Fokus:** Dalam kolaborasi tim, bagi pekerjaan berdasarkan file atau fungsi yang berbeda. Bentrok (*conflict*) hanya terjadi jika dua perubahan menyentuh **baris yang sama pada file yang sama**.
3. **Selalu Cek `git status`:** Biasakan mengetik `git status` sebelum melakukan `pull` atau berpindah *branch* untuk memastikan tidak ada perubahan lokal yang tertinggal.

---

## 4. Prosedur Darurat: Lokal & GitHub Sama-Sama Terlanjur Diedit

Jika versi lokal (VS Code) dan versi *remote* (GitHub) sama-sama sudah berubah dan isinya berbeda, ikuti langkah penyelamatan berikut:

### Tahap A: Amankan Editan Lokal & Tarik Pembaruan
* **Opsi 1: Jika editan lokal belum siap di-*commit* (pakai `stash`):**
  ```bash
  git stash
  git pull origin main
  git stash pop
  ```
* **Opsi 2: Jika editan lokal sudah siap di-*commit*:**
  ```bash
  git add .
  git commit -m "Simpan progres lokal sebelum sync"
  git pull origin main
  ```

### Tahap B: Menyelesaikan *Merge Conflict* di VS Code
Jika muncul peringatan `CONFLICT (content): Merge conflict in nama_file`, buka file tersebut di VS Code. Kamu akan melihat penanda konflik:

```text
<<<<<<< HEAD
kode versi lokal kamu di VS Code
=======
kode versi baru dari GitHub
>>>>>>> origin/main
```

**Cara menyelesaikannya:**
1. Gunakan tombol aksi cepat di atas blok konflik pada VS Code:
   * **Accept Current Change:** Pertahankan kode lokal (VS Code), buang versi GitHub.
   * **Accept Incoming Change:** Ambil kode dari GitHub, buang versi lokal.
   * **Accept Both Changes:** Gabungkan kedua versi kode tersebut.
   * *(Atau edit manual secara langsung dan pastikan tanda `<<<<<<<`, `=======`, serta `>>>>>>>` terhapus semua).*
2. Simpan file (`Ctrl + S`).
3. Finalisasi penggabungan dan *push* ke GitHub:
   ```bash
   git add .
   git commit -m "Resolve merge conflict"
   git push origin main
   ```
   *(Catatan: Jika sebelumnya memakai `git stash pop`, jalankan `git stash drop` untuk membersihkan sisa stash).*
