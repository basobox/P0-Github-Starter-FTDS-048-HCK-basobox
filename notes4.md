# Case Study: Sinkronisasi & Update Multi-Remote di Git (`origin` vs `personal`)

Dokumentasi ini merangkum studi kasus nyata dalam mengelola satu folder proyek lokal yang terhubung ke dua repositori GitHub sekaligus: repositori tugas utama (`origin`) dan repositori portofolio pribadi (`personal`).

---

## 1. Studi Kasus & Latar Belakang

* **Direktori Proyek:** `~/P0-Github-Starter-FTDS-048-HCK-basobox`
* **Branch Aktif:** `main`
* **Tujuan:** Mengirim pembaruan commit lokal ke repositori pribadi (`basobox`) tanpa mengganggu atau menghapus koneksi ke repositori tugas utama (`FTDS-Assignment-Bay-2`).

### Konfigurasi Remote (`git remote -v`)
```text
origin    git@github.com:FTDS-Assignment-Bay-2/P0-Github-Starter-FTDS-048-HCK-basobox.git (fetch)
origin    git@github.com:FTDS-Assignment-Bay-2/P0-Github-Starter-FTDS-048-HCK-basobox.git (push)
personal  git@github.com:basobox/P0-Github-Starter-FTDS-048-HCK-basobox.git (fetch)
personal  git@github.com:basobox/P0-Github-Starter-FTDS-048-HCK-basobox.git (push)
```

---

## 2. Diagnosis Kondisi Awal

Saat mengecek status repositori dengan `git status`, muncul informasi berikut:

```text
On branch main
Your branch is ahead of 'personal/main' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

### Arti Status & Simbol Terminal:
1. **Simbol `main ⇡` pada Prompt Terminal:** Menandakan ada commit di komputer lokal yang belum diunggah (*push*) ke remote.
2. **`ahead of 'personal/main' by 3 commits`:** Ada 3 commit baru di lokal yang belum masuk ke repositori `personal`.
3. **`nothing to commit, working tree clean`:** Semua perubahan file sudah di-*commit* rapi di lokal, sehingga tidak perlu menjalankan `git add` atau `git commit` lagi—cukup langsung melakukan `git push`.

---

## 3. Eksekusi Penyelesaian

Karena perubahan sudah tercatat dalam commit lokal, proses pembaruan dilakukan dengan langsung mengirim riwayat commit ke remote `personal`:

```bash
git push personal main
```

### Output Berhasil:
```text
Enumerating objects: 13, done.
Counting objects: 100% (13/13), done.
Delta compression using up to 8 threads
Compressing objects: 100% (10/10), done.
Writing objects: 100% (10/10), 3.97 KiB | 3.97 MiB/s, done.
Total 10 (delta 4), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (4/4), completed with 2 local objects.
To github.com:basobox/P0-Github-Starter-FTDS-048-HCK-basobox.git
   c9cad76..fe10adf  main -> main
```

### Verifikasi Akhir:
* Simbol panah `⇡` di prompt terminal hilang (`~/P0-Github-Starter-FTDS-048-HCK-basobox main`), menandakan lokal dan remote sudah sejajar.
* Menjalankan `git push personal main` ulang akan menghasilkan pesan **`Everything up-to-date`**.

---

## 4. Ringkasan Perintah Cepat Multi-Remote

| Tujuan Aksi | Perintah Terminal |
| :--- | :--- |
| Cek daftar remote yang terhubung | `git remote -v` |
| Cek selisih commit lokal vs remote | `git status` |
| Kirim update ke **Repo Pribadi (`basobox`)** | `git push personal main` |
| Kirim update ke **Repo Tugas (`FTDS`)** | `git push origin main` |
| Kirim update ke **Kedua Repo Sekaligus** | `git push origin main && git push personal main` |

---

## 5. Catatan Penting

* **Hindari `git remote add` Berulang:** Jika nama alias remote (`personal`) sudah terdaftar, mendaftarkannya lagi akan memicu `error: remote personal already exists`. Gunakan `git remote set-url personal <url_baru>` hanya jika ingin mengganti alamat URL-nya.
* **Cek `git status` Sebelum Commit:** Jika output menunjukkan `working tree clean`, artinya tidak ada file baru yang perlu di-`add` atau di-`commit`; kamu bisa langsung menjalankan `git push`.
