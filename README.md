
# Petunjuk Instalasi VNC, Lingkungan Desktop XFCE dan Google Chrome di VPS

Di bawah ini adalah petunjuk lengkap untuk menginstal VNC Server, menyiapkan lingkungan desktop di VPS Linux, menginstal Google Chrome, dan membuka Terminal XFCE secara otomatis saat terhubung melalui VNC.
---

### 1. Instal lingkungan desktop XFCE di VPS

Pertama, instal antarmuka grafis XFCE:

```bash
sudo apt update
sudo apt install xfce4 xfce4-goodies -y
```

### 2. Instal Server VNC

Instal VNC Server untuk mengizinkan akses jarak jauh ke antarmuka grafis VPS:

```bash
sudo apt install tightvncserver -y
```

### 3. Siapkan Server VNC

1. **Mulai VNC Server untuk pertama kalinya untuk membuat kata sandi**:

   ```bash
   vncserver
   ```

2. **Hentikan Server VNC setelah mengatur kata sandi:

   ```bash
   vncserver -kill :1
   ```

3. **Konfigurasikan VNC untuk menggunakan XFCE dan buka Terminal secara otomatis**:

   Buka file konfigurasi xstartup dan edit agar VNC memulai XFCE dengan Terminal:

   ```bash
   nano ~/.vnc/xstartup
   ```

   Ganti konten file dengan:

   ```bash
   #!/bin/sh
   xrdb $HOME/.Xresources
   startxfce4 &
   xfce4-terminal &
   ```

4. **Berikan izin eksekusi ke file tersebut `xstartup`**:

   ```bash
   chmod +x ~/.vnc/xstartup
   ```

5. **Restart VNC Server pada layar :1 (sesuai dengan port 5901)**:

   ```bash
   vncserver :1
   ```

### 4. Koneksi VNC dari mesin Windows

1. Unduh **VNC Viewer** dari [RealVNC](https://www.realvnc.com/en/connect/download/viewer/) dan instal di mesin Windows Anda.
2. Buka VNC Viewer dan sambungkan ke `IP_VPS:1`, lalu masukkan kata sandi VNC saat diminta.

   Anda sekarang akan melihat antarmuka desktop VPS dan Terminal akan terbuka secara otomatis ketika Anda masuk.

### 5. Instal Google Chrome di VPS

1. Buka Terminal (jika belum terbuka secara otomatis selama sesi VNC).
2. **Unduh Google Chrome**:

   ```bash
   wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
   ```

3. **Pasang Google Chrome**:

   ```bash
   sudo apt install ./google-chrome-stable_current_amd64.deb
   ```

   Nếu gặp lỗi phụ thuộc, chạy:

   ```bash
   sudo apt --fix-broken install
   ```

4. **Mulai Chrome di VNC** (tambahkan `--no-sandbox` jika diperlukan):

   ```bash
   google-chrome --no-sandbox
   ```

---

Dengan langkah di atas, Anda telah menyelesaikan instalasi dan dapat mengontrol VPS melalui VNC, menggunakan Google Chrome dan mengakses Terminal XFCE secara otomatis saat terhubung.
