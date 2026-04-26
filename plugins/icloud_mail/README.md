# iCloud Mail

> macOS Mail.app'teki iCloud hesabı günlük e-posta özeti.

| | |
|---|---|
| **ID** | `icloud_mail` |
| **Kategori** | Veri Kaynağı |
| **İcon** | `icloud.fill` |
| **Renk** | Mavi |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

macOS **Mail.app**'te bağlı olan iCloud hesabının `~/Library/Mail/V*/IMAP-...@imap.mail.me.com/INBOX.mbox/` veritabanını okur ve günlük e-posta aktivitesini raporlara ekler.

Rapora eklediği bilgi:

**Sabah brifingi:**
- 📧 **Gece gelen mailler** — uyandığında inbox'ta neler var
- ⭐ **Önemli/VIP** — VIP listende olan kişilerden mail varsa öne çıkar
- 🔔 **Cevap bekleyenler** — geçen günden devreden cevaplanmamış maillar

**Akşam özeti:**
- 📊 **Bugün toplamlar** — gelen sayısı, gönderdiklerinin sayısı
- 📥 **Okunmayan birikme** — günü kaç okunmamış mailla bitirdin
- 💬 **Konu kümeleri** — benzer maillerin gruplanması (örn. "5 mail e-ticaret bildirimi")

**Akıllı İşaretler:**
- 🚨 **Spam değil ama promosyonel** — ayrı bölümde özetlenir, ana akışı bozmaz
- 📅 **Toplantı daveti** — Calendar plugin'iyle çapraz referans (zaten takvimde mi?)
- 🧾 **Fatura/Ödeme** — kelime tabanlı tespit (rapora "Bu hafta 3 fatura geldi" gibi notlar)

## Gerekli İzinler

| İzin | Neden? |
|---|---|
| **Tam Disk Erişimi (Full Disk Access)** | `~/Library/Mail/` macOS sandbox'ı koruyor; FDA olmadan okunamaz. |

## Gerekli Hesaplar

| Hesap | Setup |
|---|---|
| **iCloud Mail (Apple ID)** | macOS **Sistem Ayarları > İnternet Hesapları > iCloud > Mail** açık olmalı |

## Kurulum

1. **Mağaza** > **iCloud Mail** > **Yükle**
2. **Sistem Ayarları > Gizlilik & Güvenlik > Tam Disk Erişimi** > Acciora ekle ✓
3. **Sistem Ayarları > İnternet Hesapları > iCloud > Mail** toggle'ı açık olmalı (varsayılan)
4. Mail.app'i bir kere açıp inbox'ı sync et (Acciora var olan local index'i okur)
5. **Modüller > iCloud Mail > Ayarlar > Rapor Programı**'nda toggle'ları aç

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | Mail subject, gönderen, alıcı, tarih, body (text plain) |
| **Veri nereye gider?** | Local SQLite (Acciora) → rapor için LLM'e (kullanıcı API key'i) |
| **HTML body?** | Sadece text-only kısmı LLM'e gider; resim/CSS atılır |
| **Mail attachment'leri?** | Hayır — sadece "ek var" notu, içerik okunmaz |
| **iCloud sunucusuyla doğrudan konuşur mu?** | Hayır — sadece local Mail.app'in cache'lediği veriyi okur |
| **3. parti tracking pixel?** | Mail.app zaten tracking pixel'leri block eder; Acciora etkilenmez |
| **Saklama?** | Pulse Penceresi (14 gün) sonra silinir |

## Geliştirici Notları

- Mail.app'in `Envelope Index` SQLite'ı kullanılır — emz açık olmasa bile en son sync'lenmiş veri okunabilir
- Eğer Mail.app'i hiç açmazsan veri yok (local cache boş olur)
- Multi-account destekli — bir Mail.app'te birden fazla iCloud hesabı varsa hepsi okunur
- Birden fazla Acciora hesabı yapmak için Apple ID'leri farklı kullan

## Lisans

**Plugin code:** Acciora Plugin EULA
**Mail.app SQLite schema:** Reverse-engineered
