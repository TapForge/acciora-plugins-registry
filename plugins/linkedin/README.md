# LinkedIn

> LinkedIn mesajları ve aktivite özeti.

| | |
|---|---|
| **ID** | `linkedin` |
| **Kategori** | Mesajlaşma |
| **İcon** | `briefcase.fill` |
| **Renk** | Mavi |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

LinkedIn'in resmi API'si (LinkedIn Marketing API) sıkı kısıtlamalı ve bireysel kullanıcılara açık değil. Bu plugin **WKWebView ile LinkedIn web'e giriş** + **Docker köprü konteyner** (`tomquirk-linkedin-api` Python kütüphanesi tabanlı) hybrid pattern'i kullanır — Instagram DM ile aynı yaklaşım.

Rapora eklediği bilgi:

**Sabah brifingi:**
- 💬 **Gece InMail/DM'leri** — uyurken gelen iş mesajları
- 🤝 **Yeni bağlantı istekleri** — kabul/red bekleyenler
- 📨 **Recruiter outreach** — InMail'lerden tespit (varsa)
- 🔔 **Comment notifications** — postlarına yorum gelmiş mi

**Akşam özeti:**
- 📊 **Günün LinkedIn aktivitesi** — kimle yazıştın
- ⚡ **Cevap bekleyenler** — sana yazıldı, henüz dönmedin
- 🎯 **İş teklifi/Görüşme önerisi** — kelime tabanlı tespit (LLM özet)
- 📈 **Profil view** — kim profilini görüntülemiş (LinkedIn Premium gerekir)

**Akıllı İşaretler:**
- 🆘 **Urgent ton** — "ASAP", "bugün/yarın" gibi anahtar kelimeler
- 🏢 **Şirket recruiter'ı** — "talent partner", "recruiter" unvanlı kişilerden mesajlar
- 👥 **1st-degree vs 2nd-degree** — bağlantı derecesine göre öncelik
- 📅 **Etkinlik daveti** — webinar/conference invite'ları

## Gerekli İzinler

Yok. Web tabanlı.

## Gerekli Hesaplar

| Hesap | Setup |
|---|---|
| **LinkedIn** | Hesabın olmalı, normal web giriş yapabiliyor olmalı (2FA destekli) |
| **Docker Desktop** | macOS için kurulu olmalı |

## Kurulum

1. **Docker Desktop** kur ve aç
2. **Mağaza** > **LinkedIn** > **Yükle**
3. **Modüller > LinkedIn > Hazırlık**:
   - **Docker durumu** yeşil olmalı
   - **Web girişi** → WKWebView'da `linkedin.com`'a gir, hesabınla login ol (2FA dahil)
4. **Bağlandı ✓** gör
5. **Modüller > LinkedIn > Ayarlar > Rapor Programı**'nda toggle'ları aç

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | DM/InMail metni, bağlantı isteği bilgisi (isim/unvan/şirket), notification listesi |
| **Profil view detayları?** | LinkedIn Premium ise — sadece "X kişi gördü" kısmı |
| **Post içerikleri?** | Hayır — sadece sana yorumlanan postların ID'si + comment metni |
| **Veri nereye gider?** | Docker container (local) → Acciora SQLite → LLM (kullanıcı API key'i) |
| **3. parti?** | Yok — `tomquirk-linkedin-api` açık kaynak, sadece LinkedIn ile konuşur |
| **Cookie güvenliği?** | macOS Keychain |
| **TOS riski?** | LinkedIn TOS scraping konusunda gri alan. İnsan-benzeri kullanım pattern'inde sorun çıkmaz, ama nadir hesap warning'i mümkün. |
| **Saklama?** | Pulse Penceresi (14 gün) |

## Geliştirici Notları

- LinkedIn rate limit: günde ~100 mesaj fetch (Acciora günde 6-10 atar)
- Bridge Docker image: `tapforge/acciora-linkedin-bridge:latest`
- LinkedIn web UI değişiklikleri DOM scraping'i bozabilir — plugin sürüm güncellemesi gerekir
- "Open InMail" özelliği planned — şimdilik sadece preview text okunuyor

## Lisans

**Plugin code:** Acciora Plugin EULA
**tomquirk-linkedin-api:** [MIT](https://github.com/tomquirk/linkedin-api/blob/master/LICENSE)
**Docker bridge image:** TapForge/Acciora — proprietary build
