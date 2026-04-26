# WhatsApp

> WhatsApp Web köprüsüyle DM ve grup özetleri.

| | |
|---|---|
| **ID** | `whatsapp` |
| **Kategori** | Mesajlaşma |
| **İcon** | `message.fill` |
| **Renk** | Yeşil |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

WhatsApp'ın resmi macOS uygulaması veritabanı paylaşmıyor — bu plugin **WhatsApp Web protokolü**'ne (`wacli` Go CLI'i ile) bağlanıp mesajlarını çeker. QR kodla bir kez giriş yaparsın, sonra arkaplanda DM ve grup mesajların Acciora'ya akar.

Rapora eklediği bilgi:

**Sabah brifingi:**
- 🌙 **Gece DM'leri** — uyurken gelen mesajlar
- 👥 **Önemli grup mesajları** — sabah toplantı/iş gruplarındaki cevap bekleyen konular

**Akşam özeti:**
- 💬 **Günün DM özeti** — kimle konuşuldu (içeriksiz, sadece sıklık)
- ⚡ **Geri dönüş bekleyenler** — sana yazıldı, cevaplamamışsın
- 🏘️ **Grup nabzı** — aktif gruplarda neler konuşuldu (3-5 kelimelik özet)
- 🎉 **Doğum günü/Etkinlik bahsi** — gruplarda kutlama veya plan varsa flag

**Akıllı İşaretler:**
- 🔇 **Sessize alınmış gruplar** — raporda gösterilmez (sen istedin)
- ⭐ **Favoriler** — Whatsapp'ta favori işaretledikleri ayrı vurgulanır
- 🆘 **Soru cevapsız** — soru içerikli mesajlar yanıtlanmamışsa flag
- 📞 **Sesli mesaj** — varsa "ses mesajı geldi" notu (transkripsiyon planlanan)

## Gerekli İzinler

| İzin | Neden? |
|---|---|
| **Kişiler (Contacts)** | WhatsApp telefon numaralarını kişi isimlerine eşlemek için. |

## Gerekli Hesaplar

| Hesap | Setup |
|---|---|
| **WhatsApp** | Hesabın olmalı + telefonun WhatsApp'a bağlı (web köprüsünün önkoşulu) |

## Kurulum

1. **Mağaza** > **WhatsApp** > **Yükle**
2. **wacli kurulumu** (Homebrew):
   ```bash
   brew install whatsmeow/wacli/wacli
   ```
3. **Modüller > WhatsApp > Hazırlık** > "wacli yolu" alanını otomatik doldursun (default `/opt/homebrew/bin/wacli`)
4. **WhatsApp Web girişi**:
   - **Modüller > WhatsApp > Hazırlık > QR Kodu Göster**'e bas
   - Telefonun WhatsApp uygulamasında: **Ayarlar > Bağlı Cihazlar > Cihaz Bağla**
   - Mac'teki QR'yi tara
5. "Bağlandı ✓" yeşili gör, **Modüller > WhatsApp > Ayarlar > Rapor Programı**'nda toggle'ları aç

> **Not:** WhatsApp'ın "Bağlı Cihazlar" listesinde Mac'te 1 cihaz görünür — Acciora arkaplanda çalışır, normal WhatsApp Web/Desktop kullanmaya devam edebilirsin.

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | Mesaj metni, gönderen, sohbet/grup adı, tarih |
| **Sesli mesaj/görsel içerik?** | Hayır — sadece "ek var" notu (Whisper transkripsiyon roadmap'te) |
| **Veri nereye gider?** | Local SQLite (Acciora) → rapor üretirken LLM'e gider (kullanıcının API key'i) |
| **3. parti?** | wacli açık-kaynak Go aracı, sadece WhatsApp protokolüyle konuşur. Hiçbir 3. parti sunucu yok. |
| **Şifreleme?** | E2E uçtan uca şifreleme korunur — wacli senin cihazın olarak davranır |
| **Saklama?** | Pulse Penceresi (14 gün) sonra silinir |

## Geliştirici Notları

- wacli sürekli arka planda çalışmaz — Acciora her rapor öncesi 30 saniyelik fetch çalıştırır
- WhatsApp tarafında "şüpheli aktivite" tetikleyebileceği nadir durumlar var; girişimini sık döndürürsen "telefondan onay" istenebilir
- Yeni grup eklendiğinde otomatik raporlara dahil edilir; istemiyorsan filtre ekle (planned)
- wacli bakım için bkz: https://github.com/tulir/whatsmeow

## Lisans

**Plugin code:** Acciora Plugin EULA
**wacli (whatsmeow):** [MPL 2.0](https://github.com/tulir/whatsmeow/blob/main/LICENSE)
