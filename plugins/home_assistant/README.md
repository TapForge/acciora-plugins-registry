# Home Assistant

> Akıllı ev cihazları ve sensör verilerini raporlara ekler.

| | |
|---|---|
| **ID** | `home_assistant` |
| **Kategori** | Veri Kaynağı |
| **İcon** | `house.fill` |
| **Renk** | Cyan |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

Self-hosted **Home Assistant** kurulumun varsa, Acciora bu plugin ile ev sensörlerinden ve otomasyonlarından gelen veriyi günlük raporlara ekler. Akşam raporu için özellikle değerli — günün sıcaklık ortalaması, açık/kapalı kapı sayısı, otomasyon tetikleri vs.

Rapora eklediği bilgi:

**Sadece akşam özeti (sabah/öğleye varsayılan eklenmez):**
- 🌡️ **Bugünkü sıcaklık özet** — iç/dış mekan ortalama, min/max
- 💧 **Nem & Hava kalitesi** — günlük ortalama (hassas alerji için yararlı)
- 🚪 **Açık kapı/pencere uyarıları** — gün boyunca açık kalmış olanlar
- 🔌 **Enerji tüketimi** — kWh günlük (varsa Power monitor entegre)
- 🤖 **Otomasyon tetikleri** — bugün hangi otomasyonlar çalıştı
- 🌅 **Sabah/akşam alarm tetikleri** — alarm sistemi varsa

**Akıllı İşaretler:**
- 🚨 **Anomaly** — alışılmadık sıcaklık (örn. "Salonda 30°C" sıradışı)
- 💡 **Açık kalan ışıklar** — uzun süredir on durumda olan ışıklar
- 📡 **Disconnected device** — gün içinde offline olan cihazlar
- 🌳 **Bahçe/Sera** — sensörler varsa toprak nemi vs. (özel kategori)

## Gerekli İzinler

Yok.

## Gerekli Hesaplar

| Hesap | Setup |
|---|---|
| **Home Assistant** | Self-hosted kurulumun olmalı (`homeassistant.local:8123` veya custom URL) |

## Kurulum

1. **Mağaza** > **Home Assistant** > **Yükle**
2. **Home Assistant'tan Long-Lived Access Token üret:**
   - HA web arayüzüne gir → Sol alt köşeden profil tıkla
   - **Long-Lived Access Tokens** sekmesi → "Create Token"
   - İsim: "Acciora", token'ı kopyala (sadece bir kere gösterir!)
3. **Modüller > Home Assistant > Hazırlık**:
   - **Server URL** → `https://homeassistant.local:8123` (veya kendi URL'in)
   - **Access Token** → yapıştır
   - **Bağlantıyı Test Et** → yeşil ✓ gör
4. **Modüller > Home Assistant > Ayarlar > Rapor Programı**'nda toggle'ları aç (özellikle akşam)
5. (Opsiyonel) **Hangi cihaz/entity'ler raporda?** filtresinden seç

> **Not:** Home Assistant remote access için yerel ağda olmalı veya Nabu Casa / port forwarding ile dış erişim kurmalısın.

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | Entity state'leri (sensör değerleri), automation history, energy log |
| **Veri nereye gider?** | Sadece **senin** Home Assistant kurulumun → Acciora local SQLite → rapor LLM (senin API key'inle) |
| **3. parti?** | Yok — Acciora doğrudan HA REST API'si ile konuşur (kendi cloud'u yok) |
| **Token güvenliği?** | macOS Keychain (Acciora SecureStore) |
| **HA log'larına erişim?** | Hayır — sadece state ve automation events. Tam log okunmaz. |
| **Saklama?** | Pulse Penceresi (14 gün) |

## Geliştirici Notları

- HA REST API: `/api/states`, `/api/history/period`, `/api/logbook` endpoint'leri kullanılır
- WebSocket entegrasyonu planlı (real-time sensor değişikliği — şimdi polling)
- HA Add-ons (HACS) ile çakışmaz; Acciora dış istemci olarak konuşur
- Default akşam-only çünkü ev verisi sabah brifinginde anlamlı değil; istersen sabah/öğle'ye de ekleyebilirsin

## Lisans

**Plugin code:** Acciora Plugin EULA
**Home Assistant API:** [Apache 2.0](https://github.com/home-assistant/core/blob/dev/LICENSE.md)
