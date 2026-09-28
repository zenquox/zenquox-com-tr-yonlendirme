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

## Yayın günü — Wix DNS (MX kayıtlarına dokunulmaz)

| Tür | Ad | Değer |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | zenquox.github.io |

Wix'teki eski A kayıtları (185.230.63.x) silinir. Sertifika çıkınca:
`gh api -X PUT repos/zenquox/zenquox-com-tr-yonlendirme/pages -F https_enforced=true`
