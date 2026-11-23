# Log Eksekusi Python & Git Push

## 1. Menjalankan Script Python
```bash
(base) ~/P0-Github-Starter-FTDS-048-HCK-basobox main* ❯ python app.py
hello phiTON

(base) ~/P0-Github-Starter-FTDS-048-HCK-basobox main* ❯ python app.py
hello phiTON ....
```

## 2. Mengecek Status Repository (`git status`)
```bash
(base) ~/P0-Github-Starter-FTDS-048-HCK-basobox main* ❯ git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        app.py
        notes.ipynb
        rangkuman-git-github.md

nothing added to commit but untracked files present (use "git add" to track)
```

## 3. Staging & Commit Perubahan (`git add` & `git commit`)
```bash
(base) ~/P0-Github-Starter-FTDS-048-HCK-basobox main* ❯ git add .

(base) ~/P0-Github-Starter-FTDS-048-HCK-basobox main* ❯ git commit -m "Hello phiTON ....,test2341"
[main 8c45e28] Hello phiTON ....,test2341
 3 files changed, 222 insertions(+)
 create mode 100644 app.py
 create mode 100644 notes.ipynb
 create mode 100644 rangkuman-git-github.md
```

## 4. Mengunggah ke GitHub (`git push`)
```bash
(base) ~/P0-Github-Starter-FTDS-048-HCK-basobox main ⇡ ❯ git push origin main
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (5/5), 3.07 KiB | 3.07 MiB/s, done.
Total 5 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
To github.com:FTDS-Assignment-Bay-2/P0-Github-Starter-FTDS-048-HCK-basobox.git
   8256f07..8c45e28  main -> main
```
