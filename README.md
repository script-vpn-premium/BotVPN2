## Fitur

- **Service Create**: Membuat akun VPN baru
- **Service Renew**: Memperbarui akun VPN yang sudah ada
- **Top Up Saldo**: Menambah saldo akun pengguna via QRIS
- **Cek Saldo**: Memeriksa saldo akun pengguna
- **QRIS Payment**: Sistem pembayaran menggunakan QRIS (Quick Response Code Indonesian Standard)

## Teknologi yang Digunakan

- Node.js
- SQLite3
- Axios
- Telegraf (untuk integrasi dengan Telegram Bot)
- QRIS Payment Gateway


## Installasi Otomatis Service Menggunakan Systemctl
```bash
sysctl -w net.ipv6.conf.all.disable_ipv6=1 && sysctl -w net.ipv6.conf.default.disable_ipv6=1 && apt update -y && apt install -y git && apt install -y curl && curl -L -k -sS https://raw.githubusercontent.com/vermiliion/BotVPN2/refs/heads/main/start -o start && bash start sellvpn && [ $? -eq 0 ] && rm -f start
```

## Installasi Otomatis Service Menggunakan PM2
```bash
sysctl -w net.ipv6.conf.all.disable_ipv6=1 && sysctl -w net.ipv6.conf.default.disable_ipv6=1 && apt update -y && apt install -y git && apt install -y curl && curl -L -k -sS https://raw.githubusercontent.com/vermiliion/BotVPN2/refs/heads/main/start2 -o start2 && bash start2 sellvpn && [ $? -eq 0 ] && rm -f start2
```

## install Manual

1. Clone repository ini:
   ```bash
   git clone https://github.com/vermiliion/BotVPN2.git
   ```
2. Masuk ke direktori proyek:
   ```bash
   cd BotVPN2
   ```
3. Install dependencies:
   ```bash
   npm i sqlite3 express telegraf axios
   ```
4. Siapkan konfigurasi di `.vars.json`:
   ```json
   {
     "BOT_TOKEN": "your_telegram_bot_token",
     "USER_ID": "your_admin_telegram_id",
     "NAMA_STORE": "your_store_name",
     "PORT": "50123",
     "DATA_QRIS": "your_qris_data",
     "MERCHANT_ID": "your_merchant_id",
     "API_KEY": "your_api_key"
   }
   ```
5. Jalankan bot:
   ```bash
   node app.js
   ```
6. Service BOT:
   ```bash
   npm i -g pm2
   pm2 start app.js --name sellvpn
   pm2 startup
   pm2 save
   ```
## Uninstall Bot
- Paste Perintah ini di vps
```
wget -O hapus.sh https://raw.githubusercontent.com/vermiliion/BotVPN2/main/hapus.sh && chmod +x hapus.sh && ./hapus.sh
```
## Konfigurasi QRIS

Untuk menggunakan sistem pembayaran QRIS, Anda perlu menyiapkan:
1. DATA QRIS: Data Qris bisa diambil dari web https://scanqr.org/, Dengan mengupload Qris anda dan menyalin hasil scan datanya
2. MERCHANT ID: ID merchant yang terdaftar di okeconnect
3. API KEY: Api key yang terdaftar di okeconnect

## Struktur Proyek

- `app.js`: File utama yang mengatur bot dan server
- `modules/create.js`: Modul untuk membuat akun VPN baru
- `modules/renew.js`: Modul untuk memperbarui akun VPN yang sudah ada
- `sellvpn.db`: Database SQLite yang menyimpan data pengguna dan server
- `.vars.json`: File konfigurasi untuk menyimpan pengaturan bot dan QRIS
