# Sağlık

> iPhone HealthKit verilerini sabah/akşam raporlarına ekler.

| | |
|---|---|
| **ID** | `health` |
| **Kategori** | Veri Kaynağı |
| **İcon** | `heart.fill` |
| **Renk** | Pembe |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

Apple HealthKit verilerini iOS Client uygulaması okur ve Acciora server'a senkronize eder. Bu plugin server tarafında o veriyi günlük raporlara dahil eder.

> **NOT:** Bu plugin **iOS Client** ile birlikte çalışır. iPhone'a Acciora Client uygulamasını kurmadan sağlık verisi gelmez.

Rapora eklediği bilgi:

**Sabah brifingi:**
- 😴 **Dün geceki uyku** — toplam süre, REM/Deep oranları, uyanma sayısı
- ❤️ **Dinlenme nabzı** — son 7 günle karşılaştırma
- 🛌 **Uyku kalite skoru** — Acciora'nın hesapladığı genel skor

**Akşam özeti:**
- 🚶 **Bugünkü adım** — toplam adım + hedefe kıyas
- 💓 **Kalp atış nabzı** — gün boyu ortalama, max
- 🏋️ **Egzersiz dakikası** — Apple Activity ring tamamlandı mı
- 🔥 **Aktif kalori** — günlük yakım
- 🧘 **Mood** — iOS client'tan girdiysen mood log'ları
- 💧 **Su (varsa)** — HealthKit hidrasyon log'u

**Akıllı İşaretler:**
- 📈 **Trend** — son 7 gün ortalama ile karşılaştırma (yukarı/aşağı ok)
- 🚨 **Anomaly** — istisnai yüksek nabız veya düşük uyku flag'i
- 🎯 **Hedef tutturma** — Activity ring'in tamamlanmamışsa "Yarın için motivasyon"
- 💪 **Workout tipi** — Apple Workouts'ta ne yaptın (yürüyüş/koşu/yoga)

## Gerekli İzinler (Server tarafında)

Yok — server iOS client'tan REST API ile veri alır, lokal HealthKit izni gerekmez.

## Gerekli İzinler (iOS Client tarafında)

| İzin | Neden? |
|---|---|
| **HealthKit (tüm okuma kategorileri)** | Adım, kalp, uyku, egzersiz, mood okumak için |
| **Background Refresh** | Periyodik senkron için |

## Kurulum

1. **Mağaza** > **Sağlık** > **Yükle** (server tarafında)
2. **iOS Client uygulamasını yükle** (App Store yoksa TestFlight veya enterprise)
3. iOS Client'ta:
   - **Ayarlar > Sunucu Bağlantısı** → server'a bağlan (token ile)
   - **Ayarlar > Sağlık** → "HealthKit Verisi Senkronize Et" toggle'ını aç
   - HealthKit izinleri istenir → tüm "Read" izinlerini ver
4. iOS Client arka planda her 1 saatte bir senkronize eder
5. **Modüller > Sağlık > Ayarlar > Rapor Programı**'nda sabah/akşam toggle'ları aç

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | Adım, nabız (resting + active), uyku phases, egzersiz tipi/süresi, kalori, mood, hidrasyon |
| **Tıbbi kayıt (kan tahlili, ilaç vb.)?** | **Hayır** — sadece günlük lifestyle metrik. Medical records okunmaz. |
| **Lokasyon?** | Hayır — koşu/yürüyüş GPS yolları okunmaz, sadece süre/mesafe |
| **Veri nereye gider?** | iPhone HealthKit → iOS Client → Acciora server (kullanıcının kendi local server'ı) → rapor LLM (kullanıcı API key'i) |
| **3. parti?** | Yok — Apple HealthKit + senin server, başka aracı yok |
| **iCloud sync?** | iOS HealthKit zaten Apple iCloud'a sync ediyor (sen seçtin); Acciora ek sync yapmaz |
| **Saklama?** | Pulse Penceresi (14 gün, server'da). iPhone'da Apple kuralları geçerli (manuel sil) |

## Geliştirici Notları

- iOS Client → Server REST endpoint: `POST /api/v1/health/sync` (token ile auth)
- Sabah uyku verisi: HealthKit'in `categoryTypeForIdentifier(.sleepAnalysis)` API'si ile gelir
- Apple Watch verisi varsa otomatik dahil olur (HealthKit aynı veri tabanı)
- Mood log için iOS Client'ta widget vardır (lock screen'den 1-tap mood entry)

## Lisans

**Plugin code (server):** Acciora Plugin EULA
**iOS Client:** Acciora Client EULA (App Store'dan)
**HealthKit:** Apple System Framework (kullanıcı izniyle)
