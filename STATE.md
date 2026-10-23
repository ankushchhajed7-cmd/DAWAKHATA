# DawaKhata — STATE

Medical store ke liye refill reminder PWA (single-file HTML, GitHub Pages). Patients ki regular dawaiyon ka record, kab khatam hogi uska hisaab, aur WhatsApp reminder.

## Files
- `index.html` — main app
- `demo.html` — demo version (dummy data, upar "DEMO" banner + WhatsApp link)
- `README.md`

## Version history
- **v1.1.0 (2026-10-23)** — License / activation key system poora hataya (lock screen, Device ID, activation code, `dk_key` check). App ab seedha khulta hai. `demo.html` mein bhi activation code hataya; demo ka WhatsApp link (`OWNER_WA`) rakha hai.
- **v1.0.0** — Pehla version: Due List, Patients, Report, Add/Edit, prescription photo, WhatsApp reminder, backup export/import, device-locked activation.

## Features
- **Due List** — 🔴 Late, 🟡 Aaj due, 🔵 Aane waale din (lead time ke andar)
- **Patients** — naam/mobile search, Edit, History, Refill
- **Naya patient** — naam, mobile, kai dawaiyan (naam, ₹ price, kitne din chalegi), aakhri kharid ki date
- **Refill** — due dawaiyon ki date aaj ki kar deta hai, history mein entry + total ₹
- **WhatsApp reminder** — patient ko shop naam ke saath ready message
- **Prescription photo** — camera se photo, compress karke IndexedDB mein save
- **Report** — is mahine ki sale/refills, lifetime sale, total patients, status count, top 5 dawaiyan
- **Settings** — shop naam, reminder kitne din pehle (2/3/5)
- **Backup** — JSON export/import

## Storage
- `localStorage`: `dk_patients`, `dk_settings` (demo: `dk_demo_patients`, `dk_demo_settings`)
- IndexedDB `dk_photos` → store `rx` (prescription photos, key = patient id)
- Purani keys `dk_device`, `dk_key` ab use nahi hoti (phone mein padi rahein to koi farak nahi)

## Decisions
- License key hataya — app ab free / bina lock ke chalega.

## Pending / ideas
- PWA manifest + service worker nahi hai (offline install ke liye jodna padega)
- Photos backup JSON mein shamil nahi hoti
