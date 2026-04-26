# Anımsatıcılar

> macOS Anımsatıcılar görevlerini günlük raporlara ekler.

| | |
|---|---|
| **ID** | `reminders` |
| **Kategori** | Veri Kaynağı |
| **İcon** | `checklist` |
| **Renk** | Turuncu |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

Apple **Anımsatıcılar (Reminders)** uygulamasındaki tüm aktif görevlerini izler ve günlük raporlara ekler. iCloud üzerinden iPhone, iPad, Mac arasında otomatik senkron olur — Acciora hangi cihazdan eklersen ekle aynı görevi görür.

Rapora eklediği bilgi:

**Sabah brifingi:**
- 🚨 **Süresi geçmiş** — bugün öncesi due olup tamamlanmamış görevler
- ⏰ **Bugün dolacak** — bugün için tarih atanmış görevler
- 📋 **Yaklaşan** — önümüzdeki 3 gün içindeki görevler

**Akşam özeti:**
- ✅ **Bugün tamamlanan** — gün içinde işaretlenen görevler (motivasyon için)
- ⏭️ **Yarına devreden** — bugün dolduğu halde tamamlanmayanlar (rollover)

**Akıllı İşaretler:**
- 🔁 **Tekrarlayan** — düzenli görevler ayrı işaretlenir
- 🏷️ **Liste etiketi** — "İş", "Alışveriş" gibi liste isimlerine göre gruplama
- ⭐ **Öncelik** — yüksek öncelikli görevler ayrı vurgulanır
- 📍 **Konum bazlı** — konum tetiklemeli görevler işaretlenir

## Gerekli İzinler

| İzin | Neden? |
|---|---|
| **Anımsatıcılar (Reminders)** | EventKit ile görevleri okumak için. macOS sistem ayarlarında verilir. |

## Gerekli Hesaplar

Yok. iCloud'a kayıtlıysan tüm cihazların arasında zaten senkronize.

## Kurulum

1. **Mağaza** > **Anımsatıcılar** > **Yükle**
2. Yeniden başlatma sonrası macOS **Anımsatıcılar İzni** prompt'u çıkar — **Tam Erişim** seç
3. Eğer prompt çıkmazsa: **Sistem Ayarları > Gizlilik & Güvenlik > Anımsatıcılar**'dan Acciora'yı manuel ekle
4. **Modüller > Anımsatıcılar > Ayarlar > Rapor Programı**'ndan toggle'ları aç

## iOS Client Entegrasyonu

Acciora **iOS Client** uygulamasından doğrudan görev ekleyebilirsin (push bildirimi → "Hatırlatıcı Oluştur"). Eklenen görevler iCloud üzerinden geri Mac'e senkron olur ve raporlarda görünür.

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | Görev başlığı, due date, liste, öncelik, notlar |
| **Veri nereye gider?** | Sadece local — Acciora SQLite |
| **Sunucuya senkron?** | Hayır (server zaten local) |
| **iCloud?** | Apple'ın iCloud senkronu zaten aktif (sen seçtin) |
| **3. parti?** | Hayır — EventKit sistem API'sidir |

## Geliştirici Notları

- Tamamlanmış görevler bir gün boyunca raporda kalır, sonra otomatik düşer
- "Hatırlat" notification'ları Acciora'nın push'larıyla çakışmaz (farklı kanallar)
- Plugin sadece okur — görev eklemek için iOS Client kullan veya Apple Reminders uygulamasını aç

## Lisans

**Plugin code:** Acciora Plugin EULA
**EventKit:** Apple System Framework
