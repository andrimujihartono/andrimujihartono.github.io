---
layout: post
title: "Money Tracker"
categories: project
description: "Bot Telegram untuk mencatat pemasukan dan pengeluaran otomatis ke Google Sheet."
thumbnail: /assets/img/money-tracker.png
stack:
  - Python
  - Telegram API
  - Google Sheets
---

Money Tracker adalah bot Telegram untuk mencatat pemasukan dan pengeluaran harian
langsung ke Google Sheet. Cukup kirim pesan singkat, lalu bot akan mengurai jumlah
dan kategorinya secara otomatis.

## Cara kerja

Setiap pesan masuk diproses oleh `parse_message()`, lalu hasilnya ditambahkan
sebagai baris baru. Detail lengkap ada di [dokumentasi Google Sheets API](https://developers.google.com/sheets/api).

- Kirim pesan seperti `makan siang 25000`
- Bot mendeteksi kategori dan nominal
- Data tersimpan di spreadsheet

### Contoh kode

```python
def catat(pesan):
    kategori, jumlah = parse_message(pesan)
    sheet.append_row([today(), kategori, jumlah])
    return f"Tercatat: {kategori} Rp{jumlah:,}"
```

> Tip: gunakan satu sheet per bulan agar rekap lebih mudah dibaca.

## Format pesan

| Perintah    | Contoh          | Hasil                   |
|-------------|-----------------|-------------------------|
| Pengeluaran | kopi 18000      | Dicatat sebagai keluar  |
| Pemasukan   | +gaji 5000000   | Dicatat sebagai masuk   |

## Tampilan

![Tampilan bot di Telegram]({{ '/assets/img/money-tracker-chat.png' | relative_url }})