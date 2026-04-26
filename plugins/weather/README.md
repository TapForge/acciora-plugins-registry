# Hava Durumu

> Sabah/akşam raporlarına konum bazlı hava bilgisi ekler.

| | |
|---|---|
| **ID** | `weather` |
| **Kategori** | Veri Kaynağı |
| **İcon** | `cloud.sun.fill` |
| **Renk** | Mavi |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

Hava Durumu plugin'i [Open-Meteo](https://open-meteo.com) servisinden konumuna göre **günün hava raporunu** ve **5 günlük tahmini** çeker. Sabah brifinginde "Bugün hava nasıl, ne giysem?" sorusuna yanıt verir; akşam özetinde "Yarın yağmur var mı?" planlamasını mümkün kılar.

Rapora eklediği bilgi:
- Bugün için sıcaklık aralığı (min / max)
- Şu anki hissedilen sıcaklık ve hava açıklaması (güneşli / parçalı bulutlu / yağmur / vb.)
- Yağış tahmini (saat bazlı, sabah/öğle/akşam pencereleri)
- 5 günlük özet (her gün için sıcaklık aralığı + hava durumu emoji'si)
- Anlamlı uyarılar (ekstrem sıcaklık, kar, fırtına)

## Gerekli İzinler

| İzin | Neden? |
|---|---|
| **Konum (Location)** | Eğer otomatik konum kullanmak istersen gerekir. Manuel lat/lon girersen izin gerekmez. |

> Not: Konum izni vermek istemiyorsan Ayarlar > Hava Durumu içinden manuel olarak şehir koordinatları girebilirsin. Ücretsiz lookup için [latlong.net](https://www.latlong.net).

## Gerekli Hesaplar

Yok. Open-Meteo açık API'dir, kayıt veya API key gerektirmez.

## Kurulum

1. **Mağaza** > **Hava Durumu** > **Yükle** (yeniden başlatma sonrası aktif)
2. **Modüller** > **Hava Durumu** > **Hazırlık**:
   - **Konum izni ver** (otomatik mod) VEYA
   - **Manuel koordinat** alanına şehir lat/lon değerlerini yaz
3. Sabah/akşam raporlarına eklenmesi için **Modüller > Hava Durumu > Ayarlar > Rapor Programı**'ndan toggle'ları aç

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | Sadece konum (lat/lon) |
| **Veri nereye gider?** | `api.open-meteo.com` (HTTPS) |
| **Acciora sunucusunda saklanır mı?** | Sadece günlük rapor cache'i (rapor üretildikten sonra silinebilir) |
| **3. parti analytics?** | Yok |
| **Kişisel bilgi paylaşılır mı?** | Hayır — sadece koordinat. Open-Meteo kullanıcı identity istemez. |

## Geliştirici Notları

- Konum izni reddedersen plugin offline mode'a geçer ve son cache'lenmiş hava raporunu kullanır
- Open-Meteo rate limit: günde ~10,000 istek (Acciora günde ~6 istek atar — bol bol kalır)
- 5 günlük tahmin doğruluğu Open-Meteo'nun ECMWF + GFS modelleri ile sağlanır

## Lisans

**Plugin code:** Acciora Plugin EULA (TapForge tarafından dağıtılır)
**Open-Meteo API:** [CC BY 4.0](https://open-meteo.com/en/license) (atıf raporlarda otomatik eklenir)
