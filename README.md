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

## Yayın günü (yalnızca `zenquox.com` yeni siteyle açıldıktan sonra)

1. Özel alan adını tanımla (DNS henüz Wix'i gösterse de kabul edilir):
   `gh api -X PUT repos/zenquox/zenquox-com-tr-yonlendirme/pages -f cname=zenquox.com.tr`
2. Wix DNS — **MX kayıtlarına dokunulmaz**; eski A kayıtları (185.230.63.x) ve
   `www → cdn3.wixdns.net` silinip yerine şunlar yazılır:

   | Tür | Ad | Değer |
   |---|---|---|
   | A | @ | 185.199.108.153 |
   | A | @ | 185.199.109.153 |
   | A | @ | 185.199.110.153 |
   | A | @ | 185.199.111.153 |
   | CNAME | www | zenquox.github.io |

3. DNS yayılınca sertifika kendiliğinden çıkar; ~1 saatte çıkmazsa 1. adımı yinele.
   Çıkınca HTTPS'i zorunlu kıl:
   `gh api -X PUT repos/zenquox/zenquox-com-tr-yonlendirme/pages -F https_enforced=true`

Önerilen: GitHub → Settings → Pages → *Add a domain* ile `zenquox.com.tr`'yi hesaba
doğrula (Wix'e tek bir `_github-pages-challenge-zenquox` TXT kaydı eklenir). Böylece
alan adı başka bir GitHub hesabınca sahiplenilemez.

Test (özel alan adı tanımlanana dek): https://zenquox.github.io/zenquox-com-tr-yonlendirme/
