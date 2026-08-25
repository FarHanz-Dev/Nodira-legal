# website/ — halaman publik yang WAJIB ada untuk Google Play

Tiga berkas di folder ini memenuhi dua kewajiban Play Console yang tak bisa dipenuhi dari
dalam app: **URL kebijakan privasi** dan **URL permintaan penghapusan akun**.

| Berkas | Dipakai untuk |
|---|---|
| `privacy-policy.html` | Play Console → **App content → Privacy policy** (dan tautan di store listing) |
| `account-deletion.html` | Play Console → **Data safety → Account deletion → URL permintaan penghapusan** |
| `index.html` | Halaman muka; tak diminta Play, tapi URL akar yang kosong terlihat seperti situs mati |

**Isi kedua halaman itu adalah pernyataan yang mengikat.** Ia ditulis mengikuti perilaku
kode apa adanya per 2026-08-25 (nol analytics, nol iklan, data keuangan tak pernah keluar
perangkat, daftar field Firestore persis seperti di `firebase_sync_service.dart`).
**Kalau perilaku app berubah, halaman ini ikut diubah** — deklarasi Data safety yang tak
cocok dengan perilaku app adalah alasan penolakan yang paling sering, dan yang salah
biasanya bukan app-nya melainkan dokumen yang lupa disusulkan.

---

## Cara menerbitkannya (GitHub Pages, gratis)

Repo: `FarHanz-Dev/NOTERE`. URL yang dihasilkan:

```
https://farhanz-dev.github.io/NOTERE/privacy-policy.html
https://farhanz-dev.github.io/NOTERE/account-deletion.html
```

### ⚠️ Terbitkan dari branch `gh-pages`, JANGAN dari `/docs`

GitHub Pages hanya bisa menyajikan dari **akar repo** atau folder **`/docs`** — dan
keduanya salah di repo ini:

- Menyajikan `/docs` akan **menerbitkan seluruh dokumen aturan internal** (`docs/premium.md`
  dan kawan-kawan) sebagai halaman publik yang bisa diindeks mesin pencari. Di dalamnya ada
  hal yang produk ini sengaja tak pernah tampilkan ke siapa pun — antara lain **jumlah slot
  Founding Member**, angka yang dijaga test supaya tak bocor ke UI mana pun. Menerbitkannya
  lewat pintu belakang membatalkan seluruh usaha itu.
- Menyajikan akar repo menerbitkan semuanya, termasuk `RELEASE.md`.

Karena itu situs ini hidup di branch terpisah yang **hanya berisi tiga berkas HTML**.

### Langkah sekali seumur repo

```bash
# 1. Buat branch gh-pages yang isinya HANYA folder ini
git checkout --orphan gh-pages
git rm -rf --cached . >/dev/null
git clean -fdx -e website
cp website/*.html .
rm -rf website
git add index.html privacy-policy.html account-deletion.html
git commit -m "chore(pages): halaman kebijakan privasi & penghapusan akun"
git push -u origin gh-pages
git checkout main
```

### Lalu nyalakan Pages (harus lewat browser — tak ada CLI-nya tanpa `gh`)

1. Buka **https://github.com/FarHanz-Dev/NOTERE/settings/pages**
2. **Source**: `Deploy from a branch`
3. **Branch**: `gh-pages` · **Folder**: `/ (root)` → **Save**
4. Tunggu 1–2 menit, lalu **buka kedua URL di atas dan pastikan keduanya benar-benar
   termuat.** Play memverifikasi URL-nya; halaman 404 sama saja dengan tidak mengisi.

### ⚠️ Kalau repo ini PRIVATE

GitHub Pages untuk repo private butuh **GitHub Pro/Team**. Di paket gratis, Pages hanya
jalan untuk repo **public**. Kalau repo ini private dan tak mau dipublikkan, pakai host
lain — Netlify Drop, Cloudflare Pages, atau Vercel semuanya menerima folder ini apa adanya
tanpa perubahan satu baris pun. Yang penting URL-nya publik dan tetap.

---

## Kalau berubah

Sunting berkas di `website/` pada branch `main` (di sinilah sumber kebenarannya), lalu
salin ulang ke `gh-pages`:

```bash
git checkout gh-pages
git checkout main -- website
cp website/*.html . && rm -rf website
git commit -am "chore(pages): perbarui kebijakan" && git push
git checkout main
```

**Jangan menyunting langsung di branch `gh-pages`** — perubahannya akan tertimpa pada
penyalinan berikutnya, tanpa jejak di `main`.
