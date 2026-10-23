# DawaKhata — STATE

Medical store ke liye refill reminder PWA (single-file HTML, GitHub Pages). Patients ki regular dawaiyon ka record, kab khatam hogi uska hisaab, aur WhatsApp reminder.

## Files
- `index.html` — main app
- `demo.html` — demo version (dummy data, upar "DEMO" banner + WhatsApp link)
- `README.md`

## Version history
- **v1.2.0 (2026-10-23)** — Naya **💊 Rate** tab: product naam + purchase rate list, search (live, match highlight), add/edit/delete, same naam dobara daalne pe rate update, "nahi mila" pe usi naam se jodne ka button. Backup export/import mein products shamil. Poora look ShopSathi jaisa **Silver Mirror + Gold** (mirror header + gold line, gunmetal buttons gold text, Baloo 2 font, silver mirror background). Demo mein 6 sample products.
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
- **Rate list** — product ka naam + purchase rate ₹, search box, tap karke rate badlo / delete; har product pe last update date
- **Settings** — shop naam, reminder kitne din pehle (2/3/5)
- **Backup** — JSON export/import

## Storage
- `localStorage`: `dk_patients`, `dk_products`, `dk_settings` (demo: `dk_demo_patients`, `dk_demo_products`, `dk_demo_settings`)
- IndexedDB `dk_photos` → store `rx` (prescription photos, key = patient id)
- Purani keys `dk_device`, `dk_key` ab use nahi hoti (phone mein padi rahein to koi farak nahi)

## Decisions
- License key hataya — app ab free / bina lock ke chalega.
- Theme = ShopSathi wala Silver Mirror + Gold (bg #E9EBEE, gold #D9A833, gunmetal #2A2D31).
- Rate list abhi patient ki dawai se linked nahi hai (alag list).

## Pending / ideas
- Rate list se patient form mein dawai ka naam auto-suggest
- Sale rate / MRP / margin column (abhi sirf purchase rate)
- PWA manifest + service worker nahi hai (offline install ke liye jodna padega)
- Photos backup JSON mein shamil nahi hoti
