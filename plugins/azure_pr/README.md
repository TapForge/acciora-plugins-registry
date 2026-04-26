# Azure DevOps PR

> Açık Pull Request'ler ve review ihtiyaçları.

| | |
|---|---|
| **ID** | `azure_pr` |
| **Kategori** | Üretkenlik |
| **İcon** | `arrow.triangle.pull` |
| **Renk** | Cyan |
| **Versiyon** | 1.0.0 |
| **Yazar** | TapForge |
| **Lisans** | Acciora Plugin EULA |
| **Min. Acciora** | 0.6.0 |

---

## Ne İşe Yarar?

Azure DevOps'ta **senin açtığın PR'lar** ve **sana review için atanmış PR'ları** takip eder. Aynı Azure DevOps oturumunu **Azure DevOps Efor** plugin'iyle paylaşır.

Rapora eklediği bilgi:

**Sabah brifingi:**
- 👀 **Review bekleyen (sen) PR'lar** — sabah ilk işin ne olabilir
- 💬 **Sana yorum yazılmış** — yanıtlamanı bekleyen comment'ler
- 🚨 **Conflict çıkmış** — merge öncesi çözmen gereken çakışmalar
- ⏳ **Pipeline failed** — açtığın PR'da CI kırıldıysa flag

**Akşam özeti:**
- ✅ **Bugün merged** — başarıyla merge ettiğin PR'lar
- 📊 **Açık PR sayısı** — senin açtığın + sende review olan toplam
- ⏰ **Beklemede uzun süredir** — 3+ gündür merged olmamış PR'lar
- 🎯 **Approve verdiklerin** — bugün onayladığın PR'lar

**Akıllı İşaretler:**
- 🟢 **Auto-merge eligible** — tüm checks geçmiş, approve almış (sadece "Set Auto-Complete" eksik)
- 🔴 **Reject edilmiş** — değişiklik istenmiş PR'lar
- 🆘 **Bekleyen sen değilsin** — sen approve verdin, başkası bekliyor (kim?)
- 📈 **Büyük PR** — 500+ satır değişen PR'lar (review'a daha çok zaman ayır)
- 🐌 **Stale** — 7+ gündür update edilmemiş PR'lar
- ✓ **Project bazlı sayım** — her proje için active/completed PR sayısı

## Gerekli İzinler

Yok. Web tabanlı.

## Gerekli Hesaplar

| Hesap | Setup |
|---|---|
| **Azure DevOps (Microsoft)** | Azure DevOps Efor plugin'iyle aynı hesap |

## Kurulum

> **Azure DevOps Efor plugin'i zaten yüklüyse**, bu plugin'i kurman yeterli — oturum paylaşılır, ek setup gerekmez.

1. **Mağaza** > **Azure DevOps PR** > **Yükle**
2. (Eğer Efor plugin'i yoksa) **Modüller > Azure DevOps PR > Hazırlık**:
   - Organization URL gir
   - Web girişi yap
3. **Modüller > Azure DevOps PR > Ayarlar > Rapor Programı**'nda toggle'ları aç

## Privacy

| Konu | Detay |
|---|---|
| **Hangi veri okunur?** | PR title, source/target branch, status (active/completed/abandoned), reviewer'lar, votes, comment sayısı, build status |
| **PR diff (kod) okunur mu?** | Hayır — sadece metadata. Kod değişikliği LLM'e gönderilmez. |
| **Repo isimleri?** | Evet — proje/repo bazlı raporlama için |
| **Saklama?** | Pulse Penceresi (14 gün) |

## Geliştirici Notları

- "Approve edilmiş PR'lar" silent skip değil, **ayrı kategori** (görünür kalır — auto-complete için takip)
- Project linklerine active/completed sayımı eklenir (rapora "ProjectX: 3 active, 12 completed bu hafta")
- "Effective transition" mantığı: CR → UAT geçişi sayılır, geri dönüşler hesaplanmaz (Azure efor double-count engeli)
- WKWebView session Efor plugin ile paylaşılır — login state SecureStore'da

## Lisans

**Plugin code:** Acciora Plugin EULA
