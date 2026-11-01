# Soy Atlası

Aile ağacını üç boyutlu bir takımyıldız olarak gösteren, tek dosyalık (`index.html`) ve sunucusuz bir uygulama. GitHub Gist üzerinde barınacak şekilde tasarlandı.

**Canlı:** [gist.githack.com/Runo22/8170e1784aa0638e456f607e3b2ab31b/raw/index.html](https://gist.githack.com/Runo22/8170e1784aa0638e456f607e3b2ab31b/raw/index.html) · [Gist](https://gist.github.com/Runo22/8170e1784aa0638e456f607e3b2ab31b)

## Özellikler

- **Ağaç görünümü** — her kuşak hafif kavisli tek bir sıraya dizilir: atalar yukarıda, torunlar aşağıda, baba tarafı solda, eşin ailesi sağda. Etiketler çakışmaz; ekrana sığmayanlar yakınlaştırınca görünür.
- **Pusula görünümü** — telefon için tasarlanmış, kişi merkezli gezinme. Ortada bir kişi, yukarıda ebeveynleri, yanda kardeşleri, aşağıda çocukları. Dokunulan kart ortaya geçer; ortadaki kartı sola/sağa kaydırınca kardeşler arasında gezilir, alttaki çubukta geri düğmesi ve gezinme izi var. Kartta anne, baba, eş ve çocukların **hayat çizgileri** aynı zaman ekseninde görünür; "doğduğunda annesi 25 yaşındaydı" gibi kısa bilgiler çıkarılır. Eksik ebeveyn ya da çocuk tek dokunuşla eklenir.
- **Aydınlık / koyu tema** — varsayılan aydınlık, tek tıkla koyu.
- **Fare ve trackpad** — tekerlek imlecin olduğu yere yumuşakça yakınlaşır; Shift+tekerlek ya da trackpad'de yatay kaydırma yana kaydırır; trackpad'de sıkıştırma yakınlaştırır. Sürükleyince kayar, sağ tıkla sürükleyince eğilir. Boş alana çift tık o noktaya yakınlaştırır, kişiye çift tık onu merkeze alır.
- **Gezinme düğmeleri ve mobil** — sağ altta yakınlaştır/uzaklaştır, tümünü gör, merkeze dön. Mobilde tek parmak (isimlerin üstünden de) kaydırır/döndürür, iki parmak parmakların arasına yakınlaştırır, çift dokunuş yakınlaştırır ya da kişiyi merkeze alır. Kişi kartı alt sayfa olarak açılır: tutamaçtan yukarı çekince büyür, aşağı çekince kapanır; seçilen kişi kartın üstünde görünür kalır.
- **Klavye** — `+` / `-` yakınlaştır, `0` tümünü gör, `F` merkeze dön, ok tuşları kaydır, `/` ara, `Esc` kapat. Pusula'da ↑ ebeveyne, ↓ çocuğa, ← → kardeşlere geçer, `Backspace` geri gider.
- **Yelpaze görünümü** — 7 kuşağa kadar ata yelpazesi ve torun yayı. Boş dilime tıklayarak eksik ebeveyn eklenebilir. SVG olarak dışa aktarılır.
- **e-Devlet içe aktarma** — "Alt-Üst Soy Bilgisi Sorgulama" PDF'i tarayıcıda okunur. İçe aktarmadan önce tablo gözden geçirilip düzeltilebilir.
- **Birleşen ağaçlar** — farklı kişilerin belgeleri (eş, kuzen, teyze…) ortak kişiler üzerinden otomatik birleşir. Eşleşmede ad, doğum tarihi ve baba/ana adı kullanılır. Kaçan eşleşmeler "Birleştir…" ile elle birleştirilir.
- **Herkesi merkeze alabilme** — çift tıklanan kişi ağacın merkezine geçer; tüm akrabalık adları ona göre yeniden hesaplanır (babaanne, dayı, yenge, baldız, dünür, kuzen…).
- **Elle giriş** — kişi ekleme ve düzenleme, ebeveyn/eş/çocuk/kardeş bağlama.
- **Dışa aktarma** — şifreli yedek (`.soyatlasi`, AES-256-GCM + PBKDF2), JSON, GEDCOM 5.5.1, PNG.

## Gizlilik

- Veriler yalnızca açık sekmenin belleğinde tutulur. `localStorage`, çerez veya sunucu kullanılmaz; sekme kapanınca her şey silinir.
- PDF'ler pdf.js ile tarayıcıda çözülür. Sayfadaki Content-Security-Policy, ağ isteklerini yalnızca kütüphanelerin yüklendiği CDN ile sınırlar.
- e-Devlet'in herkese açık bir API'si yok ve giriş bilgilerini bir uygulamaya vermek güvenli değil. Bu yüzden belge kullanıcı tarafından indirilip uygulamaya bırakılır.

## e-Devlet belgesini almak

1. [turkiye.gov.tr](https://www.turkiye.gov.tr) üzerinden **Alt-Üst Soy Bilgisi Sorgulama** hizmetini aç.
2. Sorguyu çalıştır ve belgeyi PDF olarak indir.
3. PDF'i uygulamaya sürükle. Başka aile bireylerinin belgelerini de ekleyebilirsin.

## Çalıştırma

Yerelde `index.html` dosyasını tarayıcıda açman yeterli. Şifreli yedek için https ya da `localhost` gerekir:

```bash
python3 -m http.server 8000
```

### Gist üzerinde yayınlama

```bash
gh gist create index.html --desc "Soy Atlası"
```

Gist'in sayfası şu adresten açılır (kullanıcı adı ve gist kimliğiyle):

```
https://gist.githack.com/<kullanıcı>/<gist-id>/raw/index.html
```

## Teknik

- [three.js](https://threejs.org) 0.160 — 3B sahne, OrbitControls, CSS2D etiketler
- [pdf.js](https://mozilla.github.io/pdf.js/) 4.10 — PDF metin çıkarma (`isEvalSupported: false`)
- Derleme adımı yok; tüm kod `index.html` içinde.
