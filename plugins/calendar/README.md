# Takvim

> macOS Takvim etkinliklerini sabah/akşam raporlarına ekler.

| | |
|---|---|
| **ID** | `calendar` |
| **Kategori** | Veri Kaynağı |
| **İcon** | `calendar` |
| **Renk** | Kırmızı |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

Apple **EventKit** üzerinden macOS Takvim uygulamasındaki tüm hesapların etkinliklerini okur. iCloud, Exchange, Google Calendar, manuel — hepsi birleşik bir görünümde.

Rapora eklediği bilgi:

**Sabah brifingi:**
- 🗓️ **Bugün** — saat sırasıyla tüm etkinlikler (yer, katılımcılar, çakışmalar işaretli)
- 📅 **Yarın** — özet liste (sürpriz olmasın diye)

**Akşam özeti:**
- 📅 **Yarın** — detay liste (hazırlık için)
- 📆 **Hafta sonu** — Cumartesi/Pazar planları

**Özel İşaretler:**
- ⚠️ **Çakışma** — aynı saatte iki etkinlik
- 🟡 **Bekleyen davet** — kabul/red yapmadığın etkinlikler
- 🔁 **Tekrarlayan** — düzenli toplantılar
- 🚗 **Seyahat** — konum belirtilmiş etkinliklere yol süresi tahmini

## Gerekli İzinler

| İzin | Neden? |
|---|---|
| **Takvim (Calendar)** | EventKit ile etkinlikleri okumak için. macOS sistem ayarlarında verilir. |

## Gerekli Hesaplar

Yok. Mevcut macOS Takvim uygulamasına bağlanır — orada ne ekliyse onu okur.

> Yeni hesap eklemek için: macOS **Sistem Ayarları > İnternet Hesapları**'ndan iCloud / Google / Exchange / vb. ekleyebilirsin. Acciora otomatik algılar.

## Kurulum

1. **Mağaza** > **Takvim** > **Yükle**
2. Yeniden başlatma sonrası macOS **Takvim İzni** prompt'u çıkar — **Tam Erişim** seç
3. Eğer prompt çıkmazsa: **Sistem Ayarları > Gizlilik & Güvenlik > Takvim**'den Acciora'yı manuel ekle
4. **Modüller > Takvim > Ayarlar > Rapor Programı**'ndan sabah/akşam toggle'larını aç

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | Etkinlik başlığı, saat, yer, katılımcı listesi, açıklama |
| **Veri nereye gider?** | Sadece local — Acciora'nın SQLite veritabanına |
| **Sunucuya senkron?** | Hayır (server zaten local) |
| **3. parti?** | Hayır — EventKit sistem API'sidir, hiçbir dış servis yok |
| **Hassas etkinlikler?** | Etkinlik notlarında kredi kartı, şifre, vs. varsa LLM'e gider (rapor özetlemesi için). Hassas içerik için private takvim kullan. |

## Geliştirici Notları

- Plugin tüm takvimlerden okur; belirli takvimleri filtrelemek için **Ayarlar > Takvim > Filtre**'yi kullan
- Tekrarlayan etkinlikler doğru handle edilir (her instance ayrı işlenir)
- Hatırlatıcılar takvimde değil, **Anımsatıcılar** plugin'inde

## Lisans

**Plugin code:** Acciora Plugin EULA
**EventKit:** Apple System Framework (kullanıcı izni ile)
