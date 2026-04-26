# Acciora Plugins Registry

> **[Acciora MacOS Server](https://acciora.app)** için resmi plugin kataloğu.

Bu repo, Acciora kişisel asistan platformu için runtime'da yüklenebilir plugin'lerin merkezi metadata kataloğunu host eder. Acciora kernel'i `index.json` dosyasını otomatik çekip Mağaza tab'ında listeler.

---

## Repo İçeriği

```
acciora-plugins-registry/
├── index.json              # Acciora kernel'inin çektiği katalog (tüm plugin'lerin metadata'sı)
├── README.md               # Bu dosya
├── LICENSE                 # Registry metadata lisansı
├── CONTRIBUTING.md         # Plugin geliştiricileri için katkı rehberi
└── plugins/
    └── <plugin-id>/
        └── README.md       # Her plugin için detaylı dökümantasyon
```

Plugin **bundle.zip** dosyaları GitHub Releases üzerinden host edilir; `index.json` içindeki `download.bundle_url` her plugin'in tag'li release'ine işaret eder.

---

## Katalog (Mevcut Plugin'ler)

Aşağıdaki plugin'ler Acciora MacOS Server v0.6.0+ ile uyumludur. Detaylı dökümantasyon için her birinin link'ine tıkla.

### 📊 Veri & Üretkenlik

| Plugin | Açıklama | Kategori |
|---|---|---|
| [Hava Durumu](plugins/weather/README.md) | Konum bazlı hava + 5 günlük tahmin | Veri |
| [Takvim](plugins/calendar/README.md) | macOS Takvim etkinlikleri & çakışmalar | Veri |
| [Anımsatıcılar](plugins/reminders/README.md) | Apple Reminders görev takibi | Veri |
| [Çağrı Notları](plugins/call_note/README.md) | Telefon arama geçmişi & cevapsız bildirimi | Üretkenlik |

### 💬 İletişim

| Plugin | Açıklama | Kategori |
|---|---|---|
| [iMessage](plugins/imessage/README.md) | macOS Mesajlar geçmişi (chat.db) | Veri |
| [WhatsApp](plugins/whatsapp/README.md) | WhatsApp Web köprüsüyle DM/grup özetleri | Mesajlaşma |
| [Instagram DM](plugins/instagram_dm/README.md) | Instagram direct mesaj özeti (Docker köprü) | Mesajlaşma |
| [LinkedIn](plugins/linkedin/README.md) | LinkedIn mesajları & bağlantı istekleri | Mesajlaşma |
| [Microsoft Teams](plugins/teams/README.md) | Teams sohbet listesi & kanal mesajları | Mesajlaşma |

### 📧 E-posta

| Plugin | Açıklama | Kategori |
|---|---|---|
| [iCloud Mail](plugins/icloud_mail/README.md) | macOS Mail iCloud hesabı günlük özeti | Veri |
| [Exchange Mail](plugins/exchange_mail/README.md) | macOS Mail Exchange kurumsal e-posta | Veri |

### 🛠️ Geliştirme & İş

| Plugin | Açıklama | Kategori |
|---|---|---|
| [Azure DevOps Efor](plugins/azure_effort/README.md) | Atanmış work item'lar & story point efor | Üretkenlik |
| [Azure DevOps PR](plugins/azure_pr/README.md) | Açık Pull Request'ler & review ihtiyaçları | Üretkenlik |

### 🏠 Yaşam

| Plugin | Açıklama | Kategori |
|---|---|---|
| [Home Assistant](plugins/home_assistant/README.md) | Akıllı ev cihazları & sensör verileri | Veri |
| [Sağlık](plugins/health/README.md) | iPhone HealthKit (adım, kalp, uyku, egzersiz) | Veri |

---

## Plugin Geliştirici misin?

Kendi plugin'ini Acciora kataloğuna submit etmek istiyorsan [CONTRIBUTING.md](CONTRIBUTING.md) rehberini takip et.

Acciora plugin SDK'sı (`AccioraPluginKit`) ve template repo bağlantıları için Acciora resmi sitesini ziyaret edebilirsin: [acciora.app/developers](https://acciora.app/developers).

---

## Güvenlik & Trust Modeli

- Tüm Acciora resmi plugin'leri **TapForge ekibi** tarafından code-signed bundle olarak dağıtılır.
- Her bundle SHA256 hash'i `index.json` içinde tutulur — Acciora kernel indirmeden önce hash'i doğrular.
- Üçüncü-parti (community) plugin'ler ayrı bir public registry'de (planlanan) tutulacak; kullanıcı kurulum öncesi onay verir.
- İmzasız veya hash uyumsuz bundle'lar reddedilir.

Detaylar için Acciora kernel kaynak kodundaki `PluginABI`, `BundlePluginLoader` ve `CodeSignatureValidator` mimarisi.

---

## Lisans

Bu repo'daki **metadata, README'ler ve `index.json`** [MIT lisansı](LICENSE) altındadır.

**Plugin bundle dosyalarının (`.bundle.zip`)** lisansı her plugin'in kendi README'sinde belirtilir. Acciora resmi plugin'leri TapForge tarafından dağıtılır ve "Acciora Plugin EULA" altındadır (kullanıcı kurulum sırasında kabul eder).

---

© 2026 TapForge — Acciora MacOS Server
