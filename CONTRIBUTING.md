# Acciora Plugin Submission Rehberi

Bu rehber, Acciora resmi kataloğuna kendi plugin'ini submit etmek isteyen geliştiriciler içindir.

---

## Genel Akış

```
1. Plugin'ini geliştir (AccioraPluginTemplate'i kullan)
   ↓
2. build-plugin.sh ile bundle.zip + SHA256 üret
   ↓
3. Bu repo'ya PR aç:
   - plugins/<id>/README.md  (yeni dosya)
   - index.json              (yeni entry)
   ↓
4. TapForge ekibi review eder
   ↓
5. Onay sonrası bundle.zip GitHub Release'e yüklenir
   ↓
6. Merge → tüm Acciora kullanıcıları Mağaza'da plugin'ini görür
```

---

## Plugin Geliştirme

Acciora plugin SDK'sı (`AccioraPluginKit` + template repo) için bkz: [acciora.app/developers](https://acciora.app/developers).

Kısa özet:
- **Dil:** Swift 5.9+
- **Platform:** macOS 14+ (arm64)
- **Format:** Dynamic library (`.dylib`) → `.bundle` paketleme
- **C ABI:** 3 sembol export edilmeli (`acciora_plugin_abi_version`, `acciora_plugin_metadata_json`, `acciora_plugin_register_v1`)
- **Code sign:** Developer ID Application sertifikan ile (yoksa self-signed da kabul, kullanıcı first-run trust dialog'unda onaylar)

---

## PR'ında Olması Gerekenler

### 1. `plugins/<your-plugin-id>/README.md`

Şu bölümleri içermeli:

```markdown
# <Plugin Adı>

> Kısa tagline (1 cümle, listing'de subtitle olarak görünür).

**ID:** `<plugin_id>`
**Kategori:** `<data_source | productivity | messaging | personal | bridge>`
**İcon:** `<SF Symbol adı>`
**Renk:** `<blue | red | green | ... >`
**Versiyon:** `<semver>`
**Yazar:** `<Adın veya organization>`
**Lisans:** `<MIT | Apache-2.0 | proprietary | ...>`

---

## Ne İşe Yarar?

2-3 paragraf detaylı açıklama. Plugin tam olarak ne yapar, hangi veri kaynaklarına bağlanır, raporlara nasıl katkıda bulunur.

## Gerekli İzinler

- `calendar` — gerekçe
- `contacts` — gerekçe

## Gerekli Hesaplar

- Microsoft Office 365 (Exchange Mail için) — kullanıcı oturum açmalı
- (varsa)

## Kurulum

Adım adım kurulum talimatları. Kullanıcı plugin'i yükledikten sonra ne yapmalı?

1. Mağaza > <Plugin Adı> > Yükle
2. Yeniden başlatmadan sonra Modüller > <Plugin Adı> > Hazırlık
3. ...

## Privacy

Bu plugin hangi veriyi okur, nereye gönderir, ne kadar saklar?

- Sadece local: ✓
- Network ister: ✓ (Open-Meteo API)
- Sunucuya hiç veri göndermez: ✓
- vs.

## Geliştirici Notları

(Opsiyonel) Bilinen sınırlamalar, gelecek sürüm planları, troubleshooting.

## Lisans

<License full text or link>
```

### 2. `index.json` Entry

`plugins` array'ine yeni bir nesne ekle:

```json
{
  "id": "my_plugin",
  "displayName": "My Plugin",
  "subtitle": "Kısa tagline",
  "description": "Detaylı açıklama (1-2 cümle)",
  "icon": "sparkles",
  "color": "purple",
  "kind": "module",
  "category": "data_source",
  "version": "1.0.0",
  "minimumAccioraVersion": "0.6.0",
  "author": "Senin Adın / Org",
  "homepage": "https://github.com/<your-namespace>/your-plugin-repo",
  "license": "MIT",
  "permissions": ["calendar", "location"],
  "download": {
    "bundle_url": "https://github.com/TapForge/acciora-plugins-registry/releases/download/my_plugin-v1.0.0/my_plugin.bundle.zip",
    "sha256": "<build-plugin.sh output>",
    "size_bytes": 234567
  }
}
```

> **NOT:** `bundle_url` Release URL'i olmalı; bundle dosyasını PR'ında commit ETME (binary'leri repo'ya koymuyoruz, GitHub Release'de host ederiz).

### 3. PR Açıklaması

Şu bilgileri ver:

- **Plugin'in ne yaptığı** (1-2 cümle özet)
- **Test prosedürü** — nasıl deneyeyim?
- **Privacy notu** — kullanıcı verisini nasıl handle ediyor?
- **build-plugin.sh çıktısı** — SHA256 + boyut

---

## Review Kriterleri

TapForge ekibi şunları kontrol eder:

- ✅ Plugin C-ABI sözleşmesine uyuyor (3 sembol export ediyor)
- ✅ ABI version `PluginABI.currentVersion` ile eşleşiyor
- ✅ Code-signed (Developer ID veya kabul edilebilir self-sign)
- ✅ README detaylı + privacy net
- ✅ index.json entry geçerli (sha256 + url + permissions)
- ✅ Plugin Acciora kullanıcısının makinesinde gerçekten yükleniyor (test edilir)
- ✅ Reasonable size (< 5 MB önerilen, > 50 MB için açıklama)

---

## Versiyon Güncellemesi

Plugin'inin yeni bir sürümünü çıkarmak için:

1. `build-plugin.sh` ile yeni bundle üret (yeni semver)
2. PR aç:
   - `plugins/<id>/README.md` versiyon ve değişiklik listesini güncelle
   - `index.json` entry'sinde `version`, `download.bundle_url`, `download.sha256`, `download.size_bytes` güncelle
3. Bundle'ı yeni Release tag'ine yükle: `<id>-v<new-version>`

Acciora kullanıcıları yeni sürümü Mağaza'da güncelleme uyarısı olarak görür (planned UX).

---

## İletişim

Sorular için: [GitHub Issues](https://github.com/TapForge/acciora-plugins-registry/issues) veya [acciora.app/contact](https://acciora.app/contact).
