# Microsoft Teams

> Teams sohbet listesi ve kanal mesajları.

| | |
|---|---|
| **ID** | `teams` |
| **Kategori** | Mesajlaşma |
| **İcon** | `person.3.fill` |
| **Renk** | Mor |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

Microsoft Teams'in resmi API'si ücretli enterprise lisans gerektiriyor. Bu plugin **WKWebView** ile Teams web sürümüne giriş yapar ve **DOM scraping** yöntemiyle sidebar'daki sohbet ve kanal aktivitesini okur. Açık kaynak Microsoft Graph API yerine browser'ın gördüğü veriyi kullanır.

Rapora eklediği bilgi:

**Sabah brifingi:**
- 💬 **Cevap bekleyen DM'ler** — sana yazıldı, görmedi/cevaplamadı
- 📢 **Önemli kanal mesajları** — @mention edildiğin gece postları
- 🔴 **Aktif rozetler** — sohbet listesinde unread badge olan kişiler

**Akşam özeti:**
- 📊 **Günün Teams aktivitesi** — kaç DM, kaç kanal mesajı
- 👥 **En aktif sohbetler** — gün içinde en sık mesaj attığın kişiler
- 🏷️ **Kanal kategorileri** — proje/ekip kanallarındaki nabız
- 🎤 **Toplantı bahsi** — kanallarda toplantı plan tartışması varsa flag

**Akıllı İşaretler:**
- @ **Mentioned** — sana @mention edildiyse vurgulanır
- 🔥 **Reactions** — yüksek reaksiyon alan mesajlar (popüler konular)
- 🆘 **Sorulu post** — "?" içeren cevaplanmamış mesajlar

## Gerekli İzinler

Yok. Hiçbir macOS sistem izni gerektirmez (web tabanlı).

## Gerekli Hesaplar

| Hesap | Setup |
|---|---|
| **Microsoft Office 365 (Teams licensed)** | İş hesabın olmalı + Teams'e web üzerinden girebiliyor olmalı |

## Kurulum

1. **Mağaza** > **Microsoft Teams** > **Yükle**
2. **Modüller > Microsoft Teams > Hazırlık > Web Girişi**:
   - Açılan WKWebView'da `teams.microsoft.com`'a gidersin
   - Microsoft hesabınla giriş yap (MFA dahil)
   - "Bağlı kal" işaretle
3. **Bağlı ✓** yeşilini gör (cookie'lar Acciora keychain'inde tutulur)
4. **Modüller > Microsoft Teams > Ayarlar > Rapor Programı**'nda toggle'ları aç

> **Not:** Teams web oturumun normal Teams desktop ile çakışmaz. Acciora arkaplanda kendi WKWebView session'ını tutar.

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | Sohbet/kanal ad, son mesaj preview, gönderen ad, badge sayıları, mention notification'ları |
| **Toplantı içeriği / Recording?** | **Hayır** — sadece chat. Toplantı kaydı, video, ses okunmaz. |
| **Dosya/Onedrive?** | Hayır — sadece sohbet metadata |
| **Cookie nereye saklanır?** | macOS Keychain (Acciora secure store). Şirket cihaz politikalarına saygı duyar. |
| **Şirket DLP?** | WKWebView default WebKit content security policy'sini kullanır; ek scraping yapmaz. Şirket compliance'ı için sen sorumlusun. |
| **3. parti tracking?** | Yok |
| **Saklama?** | Pulse Penceresi (14 gün) |

## Geliştirici Notları

- Teams web frequency throttle eder — Acciora her 15 dk'da bir hafif scrape yapar (rapor öncesi)
- Microsoft session token'ları ~30 günde bir refresh ister; expire olursa tekrar giriş yap
- DOM scraping fragile — Microsoft Teams UI güncellemesi sonrası plugin sürüm güncellemesi gerekebilir
- Toplantıların listesi için **Calendar** plugin kullan (Exchange üzerinden); Teams plugin sadece chat

## Lisans

**Plugin code:** Acciora Plugin EULA
