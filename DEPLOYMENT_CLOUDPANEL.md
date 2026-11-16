# 🚀 Panduan Deploy ke CloudPanel (pku.runforflores.com)

Landing page ini adalah **Pure Static HTML + Tailwind CSS**, sehingga sangat ringan, cepat diakses (*lightning-fast*), dan hemat resource server.

Berikut panduan langkah demi langkah untuk mendeploy ke **CloudPanel**:

---

## Langkah 1: Setting DNS Domain
Masuk ke DNS Management domain Anda (misal di Cloudflare, Niagahoster, DomaiNesia, dll) dan tambahkan record:
- **Type**: `A`
- **Name / Host**: `pku` (atau `pku.runforflores.com`)
- **IPv4 Address / Target**: Masukkan **IP Publik Server CloudPanel** Anda
- **TTL**: Auto / 3600
- *(Jika menggunakan Cloudflare, bisa gunakan status DNS Only atau Proxied)*

---

## Langkah 2: Buat Site Baru di CloudPanel
1. Buka dashboard CloudPanel Anda (biasanya di `https://IP-SERVER:8443`).
2. Klik tombol **+ Add Site** di pojok kanan atas.
3. Pilih **Create a Static HTML Site** (atau *Create a PHP Site*, keduanya bekerja optimal).
4. Masukkan konfigurasi:
   - **Domain Name**: `pku.runforflores.com`
   - **Site User**: Pilih user yang sudah ada atau buat user baru.
5. Klik **Create**.

---

## Langkah 3: Upload File ke Server
Direktori root web di CloudPanel biasanya berada di:
```text
/home/<site-user>/htdocs/pku.runforflores.com/
```

Anda bisa mengunggah file melalui salah satu cara berikut:

### Cara A: Menggunakan File Manager CloudPanel (Paling Mudah)
1. Di halaman detail site `pku.runforflores.com`, klik tab **File Manager**.
2. Masuk ke folder root `htdocs/pku.runforflores.com/`.
3. Upload file `index.html` dan seluruh isi folder `images/` (pastikan struktur foldernya tetap `images/...`).

### Cara B: Menggunakan SCP / RSYNC dari Terminal Mac Anda
Jalankan perintah ini langsung dari terminal lokal Anda (ganti `<user>` dan `<ip-server>` sesuai server Anda):
```bash
rsync -avz -e ssh index.html images/ <user>@<ip-server>:/home/<user>/htdocs/pku.runforflores.com/
```

---

## Langkah 4: Pasang SSL (HTTPS) Gratis
1. Di dashboard CloudPanel, pilih site `pku.runforflores.com`.
2. Klik tab **SSL/TLS**.
3. Klik tombol **New Let's Encrypt Certificate**.
4. Klik **Create and Install**.
5. Tunggu beberapa detik, sertifikat SSL HTTPS otomatis aktif dan auto-renew!

---

## Langkah 5: Pengujian
Buka browser dan akses:
👉 **`https://pku.runforflores.com`**

Pastikan:
- Halaman terbuka dengan protokol HTTPS aman (gembok hijau).
- Gambar poster, medali, dan jersey muncul dengan tajam.
- Saat link `https://pku.runforflores.com` dibagikan ke WhatsApp atau media sosial, pratinjau thumbnail poster dan judul resmi akan otomatis muncul karena meta tag Open Graph sudah dikonfigurasi!

