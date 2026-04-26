# iMessage

> macOS Mesajlar geçmişini günlük rapora ekler.

| | |
|---|---|
| **ID** | `imessage` |
| **Kategori** | Mesajlaşma |
| **İcon** | `message.fill` |
| **Renk** | Yeşil |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

macOS Mesajlar uygulamasının veritabanını (`~/Library/Messages/chat.db`) okuyarak iMessage ve SMS sohbetlerini günlük raporlara dahil eder. iCloud üzerinden iPhone'unla zaten senkronize olduğu için telefon ve Mac'teki mesajlar aynı görünür.

Rapora eklediği bilgi:

**Sabah brifingi:**
- 🌙 **Geceden gelen mesajlar** — uyandığında kim ne yazmış
- 💬 **Bekleyen yanıtlar** — sen yazdın, karşı taraf okudu ama cevap vermedi (vs. tersi)

**Akşam özeti:**
- 📊 **Günün sohbet özeti** — kaç kişiyle / kaç grup ile konuşuldu
- ⚡ **Geri dönüş gerek** — sana yazıldı, hâlâ cevaplamadığın
- 👥 **Aktif kişiler** — gün içinde en çok mesajlaştığın 3-5 kişi
- 🔁 **Eski sohbetlerden hareketlilik** — uzun süredir konuşmadığın biri yazdıysa flag

**Akıllı İşaretler:**
- 🆘 **Acil** — soru içerikli + cevapsız mesajlar öne çıkarılır
- 📎 **Ek var** — fotoğraf/dosya gönderilen mesajlar belirtilir
- 👨‍👩‍👧 **Aile/Yakın** — Kişiler'de favori işaretliler ayrı bölümde
- 📞 **Çağrı önerisi** — uzun mesaj zinciri varsa "X kişisini ara" hatırlatması

## Gerekli İzinler

| İzin | Neden? |
|---|---|
| **Tam Disk Erişimi (Full Disk Access)** | `~/Library/Messages/chat.db` macOS tarafından korunur; FDA şart. |
| **Kişiler (Contacts)** | Telefon/Apple ID'leri kişi isimlerine çevirmek için. |

## Gerekli Hesaplar

Yok. macOS Mesajlar uygulaman zaten Apple ID ile bağlı.

## Kurulum

1. **Mağaza** > **iMessage** > **Yükle**
2. **Sistem Ayarları > Gizlilik & Güvenlik**:
   - **Tam Disk Erişimi** > Acciora ekle ✓
   - **Kişiler** > Acciora ekle ✓
3. iCloud Mesajları aktif olmalı: iPhone **Ayarlar > [Apple ID] > iCloud > Mesajlar**
4. **Modüller > iMessage > Ayarlar > Rapor Programı**'ndan sabah/akşam toggle'ları aç

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | Mesaj metni, gönderen/alıcı, tarih, sohbet adı (grupların), ek varsa "var" notu |
| **Eklerin (foto/video) içeriği?** | **Hayır** — sadece "ek var" işareti. Görsel okunmaz, AI'ya gönderilmez. |
| **Veri nereye gider?** | Local SQLite (Acciora) → günlük rapor için LLM çağrısı |
| **LLM'e ne gider?** | Rapor üretirken sohbet özetleri Anthropic Claude'a gider (kullanıcının kendi API key'iyle, kendi hesabı altında) |
| **3. parti tracking?** | Yok |
| **Saklama?** | Pulse Penceresi (14 gün default) sonra silinir |

## Geliştirici Notları

- chat.db SQLite olduğu için read-only WAL mode'da açılır (Mesajlar uygulamasıyla çakışmaz)
- Şifrelenmiş mesajlar (Communication Safety) iCloud sync'i ile çözüldüğü için Mac'te plain okunur
- "Kaybolan mesajlar" özelliği aktifse expire olduktan sonra DB'den silinir, raporda olmaz
- Plugin sadece OKUR — mesaj göndermez

## Lisans

**Plugin code:** Acciora Plugin EULA
**chat.db schema:** Reverse-engineered (well-documented in macOS reverse-engineering community)
