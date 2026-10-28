# DawaKhata — STATE

Medical store ke liye refill reminder PWA (single-file HTML, GitHub Pages). Patients ki regular dawaiyon ka record, kab khatam hogi uska hisaab, aur WhatsApp reminder.

## Files
- `index.html` — main app
- `demo.html` — demo version (dummy data, upar "DEMO" banner + WhatsApp link)
- `README.md`
- `manifest.json`, `sw.js` — PWA install + offline
- `icons/` — `logo.svg` (master), `maskable.svg`, `icon-192.png`, `icon-512.png`, `maskable-512.png`, `apple-touch-icon.png`, `favicon-48.png`

## Version history
- **v1.7.1 (2026-10-28)** — **Screen band hone pe bill scan na tute.** Bill padhte waqt screen ON rehti hai (Chrome: Wake Lock API; APK: `ANVScreen.keepOn`), busy message mein '📱 Screen ON rakho'. Phir bhi screen band hui aur request kati to screen khulte hi apne aap dobara padhta hai. Bheji gayi photo IndexedDB `dk_scan` (store `pending`, key main/demo) mein rehti hai — app hi band ho gaya to dobara kholne pe 'Use dobara padhun?' puchta hai. Gemini ka jawab aa chuka ho to `dk_lastscan` (demo: `dk_demo_lastscan`) se check screen wapas khulti hai (24 ghante tak, Save/Cancel pe saaf). sw cache v1.7.1.
- **v1.7.0 (2026-10-28)** — **Bill scan rate fix + Gallery fix.** (1) **📐 Bill seedha karo** screen: photo chunne ke baad preview, tedhi (sideways) photo apne aap seedhi hoti hai (likhai ki lines se andaaza), ulti ho to ⟳ Ghumao; Gemini ko hamesha seedhi photo jaati hai (2400px, quality 0.9 — pehle 1800px). (2) **Gallery fix:** gallery ab ek baar mein ek photo (APK/WebView mein multi-select wala picker photo nahi lautata tha, isliye upload hi nahi hoti thi); kai page wale bill ke liye preview mein **➕ Bill ka agla page jodo** + har page pe 🗑️ Hatao. (3) **Rate cross-check:** Gemini se MRP, Rate, Sch%, DIS%, N-Rate, SGST%/CGST%/IGST%, SGST/CGST/IGST amount, Amount, Grand Total alag-alag maange jaate hain (koi hisaab Gemini nahi karta). App har line ke 4 raaste (N-Rate, Rate×(1−Sch)(1−Dis), Amount/Qty, Tax amount se) milaata hai — jo 2+ se mile wahi Net rate; GST mein sirf aadha (2.5/6/9/14) aaye to dugna; GST% galat ho to line ke tax amount se sahi slab; Sch% ko free qty samjha ho to free hata deta hai. Final = Net × (1+GST%). Shak wali line laal ⚠️, upar bill Grand Total vs App total ✓/⚠️. Test: NIDHI PHARMA bill (25 lines) — sab 25 rate sahi, bill total match. sw cache v1.7.0.
- **v1.6.0 (2026-10-23)** — Header mein **🔄 Refresh** button (⚙️ ke paas): online ho to purana cache hata ke service worker update karke reload, offline ho to bas reload (saved version khulta hai). Data (patients, rates, Gemini key, mode) safe rehta hai. sw cache v1.6.0. **Gemini auto model switch:** model na mile (404), free limit khatam (429) ya busy (500/503) ho to apne aap agla model (3.8-flash → flash-latest → 3.5-flash-lite); jawab samajh na aaye to bhi agla. Sab fail ho tabhi message (sab limit pe → 'Sabhi models ki free limit khatam', busy → '1 minute baad try karo'). Galat key pe turant message (dusre model try nahi). Check screen pe 'Model: …' dikhta hai. sw cache v1.6.1.
- **v1.5.0 (2026-10-23)** — Header ke neeche do button (Bill Photo/Gallery jaise): **💊 Rate List** (pehla) aur **👥 Patient List** (doosra); chuna hua dark gunmetal. Rate List = sirf Rate page (neeche nav nahi). Patient List = purana set (Due List, Patients, Report, Naya). App pichhli baar wala mode yaad rakhta hai (`dk_mode`), pehli baar Rate List. sw cache v1.5.0.
- **v1.4.0 (2026-10-23)** — **Mobile app icon + install**: Silver mirror + gold icon (gold medical cross pe khata lines, kone mein gunmetal badge pe capsule goli), Android gol icon ke liye alag maskable version. `manifest.json` (naam DawaKhata, standalone), `sw.js` (offline chalta hai, network-first; Gemini/WhatsApp ko nahi chhoota). Home screen pe 'Install / Add to Home screen' se app jaisa khulta hai. Demo mein bhi icon (par install manifest nahi).
- **v1.3.0 (2026-10-23)** — **📷 Bill Scan (Gemini)**: Rate tab mein "Bill Photo" / "Gallery se" (kai page ek saath). Gemini bill padh ke party naam, bill no/date, har product ka naam, qty, free, rate, disc %, GST % nikalta hai. Final rate = Rate − Disc% + GST% (free qty on ho to ×qty/(qty+free); rate na mile to amount/qty). Check screen: party naam, har line ka naam/rate edit, tick hatao, tag Naya / Purana→Naya / Same. Product ab **party-wise** save (naam + party = ek entry; alag party = alag rate). Manual form mein Party field (purani parties ki list). Search party naam se bhi. Settings mein Gemini API key + model. **Fix:** v1.1.0 mein galti se hata Settings popup wapas laaya (⚙️ button ab chalta hai). **Bug fixes (full audit):** (1) Patient edit karne pe saari dawaiyon ki date pehli dawai ki date ban jaati thi — ab date na badlo to har dawai ki apni date rehti hai, badlo to sab pe lagti hai. (2) Lamba toast message screen se bahar nahi jaata. (3) Refill/History/Report totals 2 decimal pe round (float junk nahi). (4) Gemini key URL ki jagah header (x-goog-api-key) mein; 'thinking' parts ignore; model not-found pe agla model try. Full end-to-end test (30+ checks) dono files pe pass.
- **v1.2.0 (2026-10-23)** — Naya **💊 Rate** tab: product naam + purchase rate list, search (live, match highlight), add/edit/delete, same naam dobara daalne pe rate update, "nahi mila" pe usi naam se jodne ka button. Backup export/import mein products shamil. Poora look ShopSathi jaisa **Silver Mirror + Gold** (mirror header + gold line, gunmetal buttons gold text, Baloo 2 font, silver mirror background). Demo mein 6 sample products.
- **v1.1.0 (2026-10-23)** — License / activation key system poora hataya (lock screen, Device ID, activation code, `dk_key` check). App ab seedha khulta hai. `demo.html` mein bhi activation code hataya; demo ka WhatsApp link (`OWNER_WA`) rakha hai.
- **v1.0.0** — Pehla version: Due List, Patients, Report, Add/Edit, prescription photo, WhatsApp reminder, backup export/import, device-locked activation.

## Features
- **Refresh** — 🔄 button se GitHub ka latest version turant
- **Mode switch** — upar 💊 Rate List / 👥 Patient List button; aakhri chuna mode yaad rehta hai
- **Due List** — 🔴 Late, 🟡 Aaj due, 🔵 Aane waale din (lead time ke andar)
- **Patients** — naam/mobile search, Edit, History, Refill
- **Naya patient** — naam, mobile, kai dawaiyan (naam, ₹ price, kitne din chalegi), aakhri kharid ki date
- **Refill** — due dawaiyon ki date aaj ki kar deta hai, history mein entry + total ₹
- **WhatsApp reminder** — patient ko shop naam ke saath ready message
- **Prescription photo** — camera se photo, compress karke IndexedDB mein save
- **Report** — is mahine ki sale/refills, lifetime sale, total patients, status count, top 5 dawaiyan
- **Rate list** — product + party + final purchase rate ₹, search (product ya party), tap karke rate badlo / delete; har product pe last update date
- **Bill Scan** — bill ki photo (camera / gallery, kai page) → seedha karo (auto + ⟳) → Gemini → har line cross-check (⚠️ shak) + bill total match → check screen → party-wise products save
- **Settings** — shop naam, reminder kitne din pehle (2/3/5), Gemini API key + model
- **Backup** — JSON export/import

## Storage
- `localStorage`: `dk_patients`, `dk_products`, `dk_settings` (demo: `dk_demo_patients`, `dk_demo_products`, `dk_demo_settings`)
- `dk_mode` = 'rate' / 'pat' (aakhri khula mode)
- `dk_gem` = Gemini key + model (sirf phone mein, backup mein nahi jaata)
- `dk_lastscan` = aakhri Gemini jawab jab tak Save/Cancel na ho; IndexedDB `dk_scan` → `pending` = padhne bheji bill photo (jawab aate hi delete)
- Product: `{id, name, party, rate, updated}`
- IndexedDB `dk_photos` → store `rx` (prescription photos, key = patient id)
- Purani keys `dk_device`, `dk_key` ab use nahi hoti (phone mein padi rahein to koi farak nahi)

## Decisions
- Naya version daalne pe `sw.js` mein CACHE naam (dawakhata-vX.Y.Z) badalna, taaki phone pe naya code aaye.
- License key hataya — app ab free / bina lock ke chalega.
- Theme = ShopSathi wala Silver Mirror + Gold (bg #E9EBEE, gold #D9A833, gunmetal #2A2D31).
- Rate list abhi patient ki dawai se linked nahi hai (alag list).
- Bill scan ke liye Gemini (free key, aistudio.google.com/apikey). Default model gemini-3.8-flash; 404/429/5xx pe apne aap gemini-flash-latest, phir gemini-3.5-flash-lite (Settings ka Model box khali = default).
- Ek product alag-alag party se → alag entry, taaki rate compare ho sake.
- Bill ka cash discount (poore bill pe) rate mein nahi ghataya jaata — sirf item ka Sch % / disc %.
- Final rate = Net rate (N-Rate) + GST, per unit (strip/bottle) jaisa bill mein Qty hai.
- Gemini sirf bill ke chhape number copy kare; saara hisaab app karta hai (cross-check ke saath).
- Gallery input `multiple` nahi — APK WebView (`parseResult`) multi-select (ClipData) nahi padhta.

## Pending / ideas
- Bill scan asli Gemini key ke saath aur bills pe test karna (logic NIDHI PHARMA bill data pe pass)
- apk-factory: gallery picker ClipData + multiple support (abhi app side se single photo karke bacha)
- Rate list se patient form mein dawai ka naam auto-suggest
- Sale rate / MRP / margin column (abhi sirf purchase rate)
- Photos backup JSON mein shamil nahi hoti
