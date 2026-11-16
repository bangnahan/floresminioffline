# 🚀 Panduan Lengkap Deploy ke CloudPanel dari GitHub
### Domain: `pku.runforflores.com`
### Repository: `git@github.com:bangnahan/floresminioffline.git`

---

## 📌 Alur Singkat:
1. **Setting DNS**: Arahkan subdomain `pku` ke IP VPS CloudPanel.
2. **Add Site di CloudPanel**: Buat Site Static HTML atau PHP untuk `pku.runforflores.com`.
3. **Integrasikan GitHub**: Tarik kode dari repository `floresminioffline`.
4. **Pasang SSL Let's Encrypt**: Aktifkan HTTPS gratis dalam 1 klik.

---

## 🛠️ Langkah 1: Pengaturan DNS Domain

Masuk ke panel DNS domain `runforflores.com` (Cloudflare, Niagahoster, DomaiNesia, dll) dan buat DNS Record:
* **Type**: `A`
* **Name / Host**: `pku` (menjadi `pku.runforflores.com`)
* **Target / IPv4**: Masukkan **IP Publik VPS CloudPanel** Anda
* **Proxy Status**: *DNS Only* (atau *Proxied* jika pakai Cloudflare)
* **TTL**: Auto / 3600

---

## 🌐 Langkah 2: Buat Site di CloudPanel

1. Login ke dashboard CloudPanel Anda (`https://IP-SERVER:8443`).
2. Klik tombol **+ Add Site** di pojok kanan atas.
3. Pilih **Create a Static HTML Site** (atau *PHP Site*).
4. Masukkan konfigurasi:
   * **Domain Name**: `pku.runforflores.com`
   * **Site User**: Pilih user yang ada (misal: `pku-user` atau default)
5. Klik **Create**.

---

## 🔄 Langkah 3: Deploy dari GitHub ke CloudPanel

Pilih salah satu metode di bawah ini yang paling Anda sukai:

---

### METODE A: Menggunakan SSH Langsung di Server (Paling Cepat & Simpel)

1. Buka Terminal di laptop/komputer Anda, lalu remote SSH ke server CloudPanel menggunakan user site tersebut:
   ```bash
   ssh <site-user>@<IP-SERVER-CLOUDPANEL>
   ```

2. Masuk ke direktori web root site:
   ```bash
   cd ~/htdocs/pku.runforflores.com
   ```

3. Bersihkan file default bawaan CloudPanel jika ada:
   ```bash
   rm -rf * .git*
   ```

4. Clone langsung dari GitHub:
   * **Jika repository Public / pakai HTTPS**:
     ```bash
     git clone https://github.com/bangnahan/floresminioffline.git .
     ```
   * **Jika repository Private / pakai SSH**:
     Pastikan SSH key server Anda sudah ditambahkan ke GitHub Deploy Keys, lalu jalankan:
     ```bash
     git clone git@github.com:bangnahan/floresminioffline.git .
     ```

5. **Selesai!** Berkas `index.html` dan `images/` langsung aktif.
6. *(Tips: Ke depan, jika ada perubahan kode, Anda cukup jalankan `git pull origin main` di folder tersebut).*

---

### METODE B: Menggunakan Fitur Auto-Deploy Git / Webhook CloudPanel (Otomatis Setiap Push)

Jika Anda ingin **setiap kali Anda melakukan `git push` dari laptop, website di server otomatis ter-update**:

#### 1. Pasang Deploy Key di GitHub
1. Di dashboard CloudPanel, buka site `pku.runforflores.com` ➔ klik tab **SSH / Terminal** atau **Git**.
2. Salin **Public SSH Key** yang ditampilkan di CloudPanel.
3. Buka repository GitHub Anda di browser:  
   👉 `https://github.com/bangnahan/floresminioffline` ➔ Masuk menu **Settings** ➔ **Deploy keys**.
4. Klik **Add deploy key**:
   * Title: `CloudPanel Server`
   * Key: Paste Public SSH Key tadi.
   * Allow write access: *Tidak perlu dicentang (Read-only saja)*.
   * Klik **Add key**.

#### 2. Konfigurasi Git di CloudPanel
1. Kembali ke CloudPanel pada tab **Git**.
2. Masukkan rincian:
   * **Repository**: `git@github.com:bangnahan/floresminioffline.git`
   * **Branch**: `main`
3. Pada **Deployment Script**, masukkan perintah sederhana berikut:
   ```bash
   git pull origin main
   ```
4. Klik **Save**.
5. Salin **Webhook URL** yang diberikan CloudPanel.

#### 3. Pasang Webhook di GitHub
1. Di GitHub repository `floresminioffline` ➔ **Settings** ➔ **Webhooks** ➔ **Add webhook**.
2. **Payload URL**: Masukkan Webhook URL dari CloudPanel tadi.
3. **Content type**: Pilih `application/json`.
4. **Which events**: Pilih *Just the push event*.
5. Klik **Add webhook**.

Sekarang, setiap kali Anda menjalankan `git push`, CloudPanel akan otomatis menarik pembaruan dalam hitungan detik!

---

## 🔒 Langkah 4: Pasang SSL HTTPS (Let's Encrypt)

1. Di dashboard CloudPanel, pilih site `pku.runforflores.com`.
2. Buka tab **SSL/TLS**.
3. Klik tombol **New Let's Encrypt Certificate**.
4. Klik **Create and Install**.
5. Tunggu ~10 detik. Sertifikat SSL aktif dan otomatis diperpanjang setiap 3 bulan (*auto-renewal*).

---

## ✅ Langkah 5: Pengujian Akhir

Buka browser dan akses:
👉 **`https://pku.runforflores.com`**

Periksa:
* [x] Gembok hijau HTTPS aktif.
* [x] Seluruh gambar (Logo, Poster, Medali, dan 3 Model Jersey) muncul dengan tajam.
* [x] Tombol pendaftaran mengarah ke `https://jelatix.com/event/riauforflores`.
* [x] Tombol WhatsApp mengarah ke `0811-5444-405`.
* [x] Bagikan link `https://pku.runforflores.com` ke WhatsApp untuk memastikan pratinjau thumbnail poster dan narasi pemulihan pasca gempa Flores muncul dengan menarik.
