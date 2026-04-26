# Instagram DM

> Instagram direct mesaj özeti.

| | |
|---|---|
| **ID** | `instagram_dm` |
| **Kategori** | Mesajlaşma |
| **İcon** | `camera.fill` |
| **Renk** | Pembe |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

Instagram **direct mesaj** kutusunu okur. Resmi Instagram API'si ücretsiz değil ve DM'lere izin vermiyor — bu plugin **iki katmanı** birleştirir:

1. **WKWebView ile Instagram web'e giriş** — cookie/session toplar (kullanıcının kendi credentials'ı, Acciora görmez)
2. **Docker köprü konteyner** — `instagrapi` (Python kütüphanesi) cookie ile DM API'sine erişir, Acciora'ya HTTPS ile döner

Bu hybrid yaklaşım Instagram'ın "şüpheli aktivite" tetiğine girmemek için optimize edilmiş.

Rapora eklediği bilgi:

**Sabah brifingi:**
- 💬 **Gece DM'leri** — uyurken gelen mesajlar
- 📨 **Önemli rica/iş teklifi** — uzun mesajlar veya soru içerikli yeni DM'ler
- 🆕 **Yeni mesaj isteği** — "Mesaj İstekleri" kutundaki yeniler

**Akşam özeti:**
- 📊 **Günün DM aktivitesi** — kimle yazıştın
- ⚡ **Cevap bekleyenler** — sana yazıldı, görmedin/cevaplamadın
- 🎉 **Tag/Mention** — story veya post tagleri (mention özet)
- 📷 **Reels/Post paylaşımı** — sana paylaşılanlar (URL-first format, başlık ile)

**Akıllı İşaretler:**
- ✅ **Strict filter** — yanlış güne karışan mesajlar otomatik atılır (saat normalize)
- 🎬 **Reels tespiti** — reels/post URL'leri ayrı kategoride
- 📅 **Backward timestamp inheritance** — grup mesajları sırası bozulmaz
- 🔄 **SPA geç render** — Instagram web yavaş render ettiğinde otomatik retry

## Gerekli İzinler

Yok. Web tabanlı.

## Gerekli Hesaplar

| Hesap | Setup |
|---|---|
| **Instagram** | Hesabın olmalı + 2FA olmadan giriş yapabiliyor olmalı (2FA'lı hesaplar şu an desteklenmiyor — planlanan) |
| **Docker Desktop** | macOS için kurulu olmalı (`docker.com/products/docker-desktop`) |

## Kurulum

1. **Docker Desktop** kur ve aç (`https://docker.com/products/docker-desktop`)
2. **Mağaza** > **Instagram DM** > **Yükle**
3. **Modüller > Instagram DM > Hazırlık**:
   - **Docker durumu** yeşil olmalı (Acciora docker connect olduğunu kontrol eder)
   - **Web girişi** → WKWebView'da `instagram.com`'a gir, hesabınla login ol
4. **Bağlandı ✓** gör (cookie'lar Acciora keychain'inde, instagrapi container'a aktarılır)
5. **Modüller > Instagram DM > Ayarlar > Rapor Programı**'nda toggle'ları aç

> **İlk ne kadar sürer?** Docker container ilk kez ~500 MB image indirir. Sonraki açılışlar saniyeler içinde.

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | DM metni, gönderen username, tarih, paylaşılan reels/post URL'leri |
| **Foto/Video içerik?** | Hayır — sadece "ek var" notu |
| **Story görüntüleme?** | Hayır — sadece kendine gelen story tag'leri |
| **Veri nereye gider?** | Docker container (local) → Acciora SQLite → rapor LLM (kullanıcı API key'i) |
| **Instagram dışı 3. parti?** | Yok — instagrapi açık kaynak, sadece Instagram API'si ile konuşur |
| **Cookie/Session güvenliği?** | macOS Keychain (Acciora SecureStore) |
| **Şüpheli aktivite riski?** | Düşük — instagrapi insan benzeri davranışı taklit eder. Yine de Instagram TOS gri alanı. |
| **Saklama?** | Pulse Penceresi (14 gün) |

## Geliştirici Notları

- Instagram DM API rate limit: ~200 istek/saat (Acciora günde 6-10 atar — bol kalır)
- 2FA hesaplar için "App Password" mekanizması Instagram tarafından henüz açılmadı; bu yüzden 2FA kapalı hesaplar gerek
- Bridge Docker image: `tapforge/acciora-instagram-bridge:latest` (Docker Hub'da public)
- Eğer Instagram "şüpheli aktivite" mailı gönderirse Acciora'yı 24 saat duraklat ve normal browserda giriş yap

## Lisans

**Plugin code:** Acciora Plugin EULA
**instagrapi:** [MIT](https://github.com/subzeroid/instagrapi/blob/master/LICENSE)
**Docker bridge image:** TapForge/Acciora — proprietary build
