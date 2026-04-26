# Exchange Mail

> macOS Mail'deki Exchange hesabı günlük e-posta özeti.

| | |
|---|---|
| **ID** | `exchange_mail` |
| **Kategori** | Veri Kaynağı |
| **İcon** | `envelope.badge.fill` |
| **Renk** | Mavi |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

macOS **Mail.app**'te bağlı **Microsoft Exchange (Office 365)** hesabının kurumsal e-posta akışını okuyup günlük raporlara ekler. iCloud Mail plugin'iyle aynı pattern'i kullanır ama Exchange-spesifik özellikleri (toplantı daveti, mention'lar, kategoriler) ayrı işler.

Rapora eklediği bilgi:

**Sabah brifingi:**
- 📧 **Gece gelen iş mailleri** — pazartesi sabahları özellikle yararlı
- 🚨 **Yöneticinden mail** — manager'ından gelen mailler ayrı vurgulanır (Kişiler'de işaretlersen)
- 📅 **Toplantı daveti bekliyor** — kabul/red yapmadığın Exchange davetleri

**Akşam özeti:**
- 📊 **Bugün toplam** — gelen, gönderilen, cevaplanan, okunmayan birikme
- 💬 **Konu klasörleri** — Outlook kategorilerine göre gruplama (Müşteri, Proje X, vs.)
- ⏰ **OOO (Out of Office) bildirimleri** — kimler yokmuş bugün
- 🎯 **Bekleyen aksiyon** — sana atanmış görev içerikli mailler

**Akıllı İşaretler:**
- 🔥 **High Importance** — Outlook'un "yüksek öncelikli" flag'ı taşıyan mailler
- 📞 **Toplantı önerisi** — "Müsait misin Cuma?" tarzı mailler ayrı bölümde
- 👥 **Mention** — "@SeninAdın" geçen group mailler vurgulanır
- 🏢 **Internal vs External** — şirket dışından gelen mailler ayrı kategori

## Gerekli İzinler

| İzin | Neden? |
|---|---|
| **Tam Disk Erişimi (Full Disk Access)** | `~/Library/Mail/V*/EWS-*` korumalı; FDA gerekir. |

## Gerekli Hesaplar

| Hesap | Setup |
|---|---|
| **Microsoft Office 365 / Exchange** | macOS **Sistem Ayarları > İnternet Hesapları > Exchange** üzerinden eklenmiş olmalı |

## Kurulum

1. **Mağaza** > **Exchange Mail** > **Yükle**
2. **Sistem Ayarları > İnternet Hesapları > Exchange Hesabı Ekle**:
   - İş e-postan + parola gir
   - "Mail" toggle'ını aç (Calendar/Reminders/Contacts opsiyonel)
3. Mail.app'i aç, Exchange inbox'ının sync olmasını bekle (5-10 dk)
4. **Sistem Ayarları > Gizlilik & Güvenlik > Tam Disk Erişimi** > Acciora ekle ✓
5. **Modüller > Exchange Mail > Ayarlar > Rapor Programı**'nda toggle'ları aç

> **Modern Auth Sorunu?** Şirketin MFA/Conditional Access politikası varsa "Apple Mail" için exception gerekebilir. IT'ye sor.

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | Subject, gönderen, alıcı, tarih, body text, kategori, importance |
| **Şirket sunucusuyla bağlantı?** | Hayır — Mail.app'in zaten yaptığı IMAP/EWS sync'inden cached veri okunur |
| **LLM'e ne gider?** | Mail subject + özet body, kullanıcının API key'i ile (Anthropic Claude). Şirket compliance'ı için kullanıcı sorumlu. |
| **Şirket DLP?** | Mail.app local cache'i okumak DLP'yi tetiklemez (zaten cihazda olan veri) |
| **Saklama?** | Pulse Penceresi (14 gün) sonra silinir |

## Geliştirici Notları

- iCloud Mail plugin ile aynı kod yolu — sadece account filter farklı
- Exchange categories `flag.color` mapping'i ile rapora taşınır (örn. "Kırmızı = Acil")
- Calendar entegrasyonu Exchange üzerindeki davetleri ayrı handle eder (Calendar plugin)
- Bazı kurumsal Mail.app config'leri local cache'i devre dışı bırakır — bu durumda plugin çalışmaz

## Lisans

**Plugin code:** Acciora Plugin EULA
**Mail.app SQLite schema:** Reverse-engineered (iCloud Mail ile aynı)
