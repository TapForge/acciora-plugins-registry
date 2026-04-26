# Çağrı Notları

> Telefon arama geçmişi ve çağrı bildirimleri.

| | |
|---|---|
| **ID** | `call_note` |
| **Kategori** | Üretkenlik |
| **İcon** | `phone.fill` |
| **Renk** | Yeşil |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

macOS'ın **Çağrı Geçmişi veritabanı** (`~/Library/CallHistoryDB/CallHistory.storedata`) iPhone'undan FaceTime ile senkronize olan tüm gelen/giden aramaları tutar. Bu plugin o veriyi okuyup günlük raporlara ve gerçek zamanlı bildirimlere çevirir.

**3 ana iş:**

1. **Cevapsız arama push'u** — Mac'te konferansta veya odaklanma modundayken cevaplayamadığın çağrılar için iOS client'a push bildirimi atar (gecikmesiz, real-time).

2. **Günlük arama özeti** — Akşam raporunda:
   - Bugün toplam arama sayısı (gelen / giden / cevapsız)
   - Toplam konuşma süresi
   - En sık konuşulan 3-5 kişi
   - Önemli aramalar (uzun süreli, iş kontaktları)

3. **Etkileşim notları** — Her çağrı kişi profiline interaction olarak yazılır (Acciora'nın "Kişiler" sekmesinde gözükür, "X kişisiyle 3 gündür konuşmadım" gibi insight'lar üretir).

## Gerekli İzinler

| İzin | Neden? |
|---|---|
| **Tam Disk Erişimi (Full Disk Access)** | `~/Library/CallHistoryDB/` macOS tarafından korunur; FDA olmadan okunamaz. |
| **Kişiler (Contacts)** | Telefon numaralarını isimlere çevirmek için. |

> **FDA Setup:** Sistem Ayarları > Gizlilik & Güvenlik > Tam Disk Erişimi > Acciora'yı ekle ve toggle'ı aç. Yeniden başlatma gerekebilir.

## Gerekli Hesaplar

Yok. iPhone-Mac FaceTime senkronu zaten Apple ID üzerinden çalışıyor.

## Kurulum

1. **Mağaza** > **Çağrı Notları** > **Yükle**
2. Yeniden başlatma sonrası **Sistem Ayarları > Gizlilik & Güvenlik**:
   - **Tam Disk Erişimi** > Acciora ekle ✓
   - **Kişiler** > Acciora ekle ✓
3. iPhone'da: **FaceTime > Tercihler > "Mac'te de çağrılar"** açık olmalı
4. Test et: Modüller > Çağrı Notları > Hazırlık'ta "Veritabanı erişimi" yeşil olmalı
5. Bildirimleri istersen: **Modüller > Çağrı Notları > Ayarlar > Cevapsız Push** toggle'ını aç

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | Çağrı tarihi, süresi, telefon numarası, yön (gelen/giden/cevapsız) |
| **Çağrı içeriği?** | **Hayır** — sadece metadata. Konuşma kaydı yapılmaz, dinlenmez. |
| **Veri nereye gider?** | Local SQLite (Acciora) + iOS push (sadece cevapsız bildirimi için) |
| **3. parti?** | Hayır |
| **Saklama?** | Acciora'nın "Pulse Penceresi" (default 14 gün) süresince. Sonra otomatik silinir. |

## Geliştirici Notları

- macOS güncellemeleri sonrası FDA izni reset olabilir — kontrol et
- Çağrı geçmişi ~5-10 saniye gecikmeyle yansır (FaceTime senkron süresi)
- Numara → kişi eşleşmesi için Kişiler izni şart, yoksa sadece "+90 5xx ..." görünür
- Kişi profilinde "Son arama" tarihi ve sıklığı analytics olarak işlenir

## Lisans

**Plugin code:** Acciora Plugin EULA
**CallHistoryDB schema:** Reverse-engineered from public macOS internals
