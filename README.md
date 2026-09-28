# zenquox.com.tr → zenquox.com yönlendirmesi

`zenquox.com.tr` alan adının DNS'i Wix'te kalır; yalnızca web kayıtları bu GitHub Pages
sitesine çevrilir. Buradaki sayfalar ziyaretçiyi anında `zenquox.com`'a gönderir
(anlık meta refresh + JavaScript; Google anlık meta refresh'i kalıcı yönlendirme sayar).

## Eşleme

| Eski (zenquox.com.tr) | Yeni (zenquox.com) |
|---|---|
| `/` | `/` (sorgu dizesi korunur) |
| `/hakkımızda` | `/#hakkimizda` |
| `/hizmetlerimiz` | `/#hizmetler` |
| `/hemen-başlayın` | `/#iletisim` |
| `/book-online` | `/#iletisim` |
| `/gizlilik-politikası` | `/gizlilik/` |
| `/çerez-politikası` | `/gizlilik/` |
| `/erişilebilirlik-beyanı` | `/` |
| `/service-page/…` | `/#iletisim` |
| `/hizmetler/…`, `/projeler/…`, `/gizlilik/…` | aynı yol |
| diğer her şey | `/` |

## Durum — yayında (28 Eylül 2026)

- Özel alan adı `zenquox.com.tr` (depodaki `CNAME`); `www` → apex yönlendirmesini GitHub yapar.
- Sertifika Let's Encrypt (`zenquox.com.tr`, `www.zenquox.com.tr`), GitHub kendiliğinden yeniler; HTTPS zorunlu.
- Wix DNS'teki web kayıtları aşağıdaki gibidir. **MX ve TXT kayıtlarına dokunulmaz** (Google Workspace);
  alan adı Wix'ten **silinmez** — DNS orada barınır.

  | Tür | Ad | Değer |
  |---|---|---|
  | A | @ | 185.199.108.153 · 185.199.109.153 · 185.199.110.153 · 185.199.111.153 |
  | CNAME | www | zenquox.github.io |

## Sertifika sorunu olursa

- Özel alan adı DNS değişmeden tanımlanırsa sertifika talebi başlamaz; aynı değerle yeniden kaydetmek de
  tetiklemez. Kaldırıp yeniden ekle (arada birkaç saniye yanıt vermez):
  `gh api -X PUT repos/zenquox/zenquox-com-tr-yonlendirme/pages -F cname=null` →
  `gh api -X PUT repos/zenquox/zenquox-com-tr-yonlendirme/pages -f cname=zenquox.com.tr`
- Durumu izle: `gh api repos/zenquox/zenquox-com-tr-yonlendirme/pages --jq .https_certificate.state`.
  Çalışan sertifika `approved`'da kalabilir; o noktada HTTPS'i zorunlu kıl:
  `gh api -X PUT repos/zenquox/zenquox-com-tr-yonlendirme/pages -F https_enforced=true`
- GitHub'ın DNS görüşü: `gh api repos/zenquox/zenquox-com-tr-yonlendirme/pages/health` (Wix TTL'i 1 saat).

Önerilen: GitHub → Settings → Pages → *Add a domain* ile `zenquox.com.tr`'yi hesaba
doğrula (Wix'e tek bir `_github-pages-challenge-zenquox` TXT kaydı eklenir). Böylece
alan adı başka bir GitHub hesabınca sahiplenilemez.
