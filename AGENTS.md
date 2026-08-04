# 🤖 AI Coding Agent Guidelines

Dokumen ini berisi standar kerja & aturan wajib bagi AI Agent di repository ini.

---

## 1. Project Context & Environment

- **Environment:** Sesuaikan dengan project (Linux/VPS, Docker, cloud, dsb). Cek `README.md` atau file konfigurasi (`.env.example`, `docker-compose.yml`, `package.json`, dll) sebelum mulai kerja untuk memahami stack yang dipakai.
- **Project Type:** Isi sesuai project — web app, mobile app, CLI tool, API service, dsb. Jangan asumsikan stack tanpa mengecek terlebih dahulu.
- Gunakan environment variables (`.env`) untuk data sensitif. **Jangan pernah** menyimpan kredensial, API key, token, atau secret lain langsung di dalam kode atau di-commit ke repo.
- Jika project punya dokumen perencanaan (`PRD.md`, `AGENT_PLAN.md`, `CLAUDE.md`, dsb), baca dulu sebelum membuat perubahan besar — dokumen ini jadi acuan arsitektur dan scope.

---

## 2. Code Quality & Security

- Tulis kode yang modular, mudah dibaca, konsisten dengan konvensi yang sudah ada di codebase (penamaan, struktur folder, style formatting).
- Aman dari kerentanan umum: SQL Injection, XSS, command injection, insecure deserialization, path traversal, dsb — sesuaikan dengan risiko yang relevan untuk stack yang dipakai.
- Sebelum menyelesaikan tugas, pastikan kode:
  - Bebas dari error sintaks (linter/compiler check sesuai bahasa: `eslint`, `tsc`, `ruff`, `go vet`, `php -l`, dll).
  - Lulus unit test/test suite yang ada, jika tersedia.
  - Tidak menghapus atau merusak fungsionalitas yang sudah berjalan tanpa instruksi eksplisit.
- Jangan menambahkan dependency baru tanpa alasan jelas — cek dulu apakah kebutuhan sudah bisa dipenuhi dengan tooling yang ada.

---

## 3. Git Workflow & CI/CD Trigger

1. **Granular Commit:** Lakukan `git commit` untuk setiap 1 tugas/fitur kecil yang selesai dikerjakan. Gunakan format Conventional Commits (`feat: ...`, `fix: ...`, `chore: ...`, `refactor: ...`, `docs: ...`).
2. **Push ke remote** hanya setelah komit dipastikan bebas error dan (jika ada) lulus test lokal:
   `git push origin main` (atau branch kerja sesuai konvensi tim/project — cek dulu apakah repo pakai trunk-based atau feature-branch workflow).

   > ⚠️ **Catatan:** Jika repo punya pipeline CI/CD (GitHub Actions, GitLab CI, dsb), `git push` bisa memicu deploy otomatis. Pastikan perubahan benar-benar siap sebelum push ke branch yang terhubung ke pipeline deploy.
3. Jika project menggunakan pull request/merge request workflow, jangan push langsung ke `main`/`master` kecuali diinstruksikan — buat branch dan PR sesuai konvensi repo.

---

## 4. Restrictions (Yang Dilarang)

- ❌ Dilarang `git push` jika kode masih bermasalah, gagal build, atau gagal test.
- ❌ Dilarang menjalankan perintah destruktif (`rm -rf`, `DROP DATABASE`, `git push --force`, overwrite file besar-besaran, dll) tanpa persetujuan eksplisit dari user.
- ❌ Dilarang mengubah struktur folder utama, arsitektur inti, atau dependency versi mayor tanpa instruksi spesifik.
- ❌ Dilarang mengekspos atau mencetak (log/print) kredensial dan data sensitif, bahkan untuk debugging.
- ❌ Dilarang menginstal atau menjalankan package/skrip pihak ketiga yang tidak terverifikasi tanpa konfirmasi user.

---

## 5. Communication

- Jika instruksi ambigu atau ada beberapa pendekatan valid, jelaskan asumsi yang diambil lalu lanjutkan — jangan berhenti total tanpa progres.
- Laporkan ringkas apa yang diubah, kenapa, dan file mana saja yang terdampak setelah tugas selesai.
- Jika menemukan bug atau isu lain di luar scope tugas saat ini, catat/laporkan tapi jangan langsung diperbaiki kecuali diminta.
