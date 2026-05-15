# Auto Commit

Repositori kecil untuk menjalankan commit otomatis lewat GitHub Actions. Workflow akan memperbarui berkas `LAST_UPDATED`, membuat commit dengan pesan acak bernuansa bahasa Indonesia, lalu mendorong perubahan ke branch `main`.

## Jadwal

Workflow berjalan otomatis setiap hari pada:

- `07:00 UTC` / `14:00 WIB`
- `09:00 UTC` / `16:00 WIB`
- `11:00 UTC` / `18:00 WIB`
- `15:00 UTC` / `22:00 WIB`

Konfigurasi cron ada di `.github/workflows/auto_commit.yml`:

```yml
schedule:
  - cron: "0 7,9,11,15 * * *"
```

## Token

Workflow memakai `GITHUB_TOKEN` bawaan GitHub Actions. Token ini otomatis tersedia di setiap workflow, jadi tidak perlu membuat secret manual.

Pastikan izin workflow sudah bisa menulis ke repositori:

1. Buka `Settings` repositori.
2. Pilih `Actions` → `General`.
3. Pada `Workflow permissions`, pilih `Read and write permissions`.

## Menjalankan Manual

Workflow juga bisa dijalankan manual dari GitHub:

1. Buka tab `Actions`.
2. Pilih workflow `Auto commit`.
3. Klik `Run workflow`.
4. Pilih branch `main`.
5. Klik `Run workflow`.

## Cara Kerja

1. Checkout branch `main`.
2. Isi ulang `LAST_UPDATED` dengan waktu UTC terbaru.
3. Pilih pesan commit acak.
4. Commit perubahan.
5. Push kembali ke repositori.

## Catatan

- Jadwal GitHub Actions memakai zona waktu UTC.
- Eksekusi cron bisa terlambat beberapa menit.
- Scheduled workflow bisa berhenti otomatis jika repositori lama tidak aktif.
- Jika run manual sukses, cron biasanya ikut berjalan sesuai jadwal.
