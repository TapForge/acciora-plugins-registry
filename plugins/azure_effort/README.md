# Azure DevOps Efor

> Atanmış work item'lar ve story point efor takibi.

| | |
|---|---|
| **ID** | `azure_effort` |
| **Kategori** | Üretkenlik |
| **İcon** | `shippingbox.fill` |
| **Renk** | Cyan |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

Azure DevOps web sürümüne **WKWebView** ile giriş yapıp sana **atanmış User Story / Bug / Task** work item'larını listeler. Her item'ın **Story Point** veya **Effort** alanına bakarak günlük/haftalık çalışma yükünü hesaplar.

Rapora eklediği bilgi:

**Sabah brifingi:**
- 📦 **Bugün üzerinde çalışılacaklar** — In Progress + sana atanmış
- 🎯 **Story Point yükü** — bu sprint için kalan SP
- 🚨 **Geciken işler** — due date geçmiş ama hâlâ açık item'lar
- 🆕 **Dün atanan** — son 24 saatte sana yeni atanmış işler

**Akşam özeti:**
- ✅ **Bugün biten** — Done'a alınmış item'lar (motivasyon!)
- 📊 **Sprint nabzı** — kaç SP yapıldı, kaç SP kaldı
- ⏳ **Code Review bekliyor** — done dediğin ama PR review'da takılı işler
- 🔄 **Tekrar açıldı** — done iken reopen edilmişse (regression flag)

**Akıllı İşaretler:**
- 🔥 **Yüksek öncelik** (Priority 1/2) — özel vurgu
- 🐛 **Bug** (özel kategori) — taze bug'lar veya sürükleyen bug'lar
- 📝 **Açıklama yetersiz** — story description boşsa flag (acceptance criteria yok)
- 👥 **Engelleyen başkası** — "Blocked by" relation varsa kim engelliyor not edilir

## Gerekli İzinler

Yok. Web tabanlı.

## Gerekli Hesaplar

| Hesap | Setup |
|---|---|
| **Azure DevOps (Microsoft)** | Şirket Azure DevOps organization'ına erişimin olmalı (`dev.azure.com/{org}` veya `{org}.visualstudio.com`) |

## Kurulum

1. **Mağaza** > **Azure DevOps Efor** > **Yükle**
2. **Modüller > Azure DevOps Efor > Hazırlık**:
   - **Organization URL** → şirket Azure DevOps URL'ini gir (`https://dev.azure.com/<org-name>`)
   - **Project Name** → varsayılan proje (boş bırakırsan tüm projeler taranır)
3. **Web Girişi** → WKWebView açılır, Microsoft hesabınla gir (MFA dahil)
4. **Bağlı ✓** yeşilini gör
5. **Modüller > Azure DevOps Efor > Ayarlar > Rapor Programı**'nda toggle'ları aç

> **NOT:** Bu plugin Azure DevOps PR plugin'iyle **aynı oturumu paylaşır** — bir kere giriş yaparsan ikisi de çalışır.

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | Work item title, ID, type (Story/Bug/Task), state, story point/effort, assigned to, due date, description |
| **Tam description body LLM'e mi gider?** | Sadece **özet** (ilk 200 karakter). Kapsamlı description için işin Azure'da görüntülenir. |
| **Şirket DLP?** | WKWebView session'ı normal browser oturumudur; ek bir scraping yapılmaz. Compliance için kullanıcı sorumlu. |
| **Veri nereye gider?** | Local SQLite + rapor LLM çağrısı |
| **Saklama?** | Pulse Penceresi (14 gün) |

## Geliştirici Notları

- Sprint cycle'ı otomatik algılanır (Iteration Path'ten)
- Custom field'lar (örn. "Effort Hours" yerine "Story Points") konfigüre edilebilir
- Multi-org desteklenmiyor (1 org / 1 hesap) — ileride planned
- Microsoft session token ~30 günde refresh ister; expire'da tekrar giriş

## Lisans

**Plugin code:** Acciora Plugin EULA
