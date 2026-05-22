# sehlaayardimet.github.io

Şəhla Ağayeva üçün xeyriyyə saytı. Pure static — `index.html` + `style.css` + `script.js` + `/images`. Heç bir build tool, framework və ya npm paketi yoxdur. Birbaşa brauzerdə də açılır, GitHub Pages-də də işləyir.

## Fayl strukturu

```
sehlaayardimet.github.io/
├── index.html        ← bütün məzmun (4 dil üçün eyni HTML)
├── style.css         ← stillər (mobile-first, ~360px-dən başlayır)
├── script.js         ← dil dəyişdirici + kart nömrəsi kopyalama
├── images/
│   ├── photo-1.jpg   ← (sən əlavə edirsən — paylaşıldıqda görünən)
│   ├── photo-2.jpg
│   ├── photo-3.jpg
│   └── photo-4.jpg
└── README.md         ← bu fayl
```

---

## 1. Müalicə mərhələlərini necə əlavə etmək olar

Mərhələlər birbaşa `index.html` daxilindədir, `<ol class="timeline-steps">` daxilində. Yeni mərhələ əlavə etmək üçün eyni şablondan bir `<li>` kopyala:

```html
<li class="step completed">
  <span class="step-dot" aria-hidden="true"></span>
  <div class="step-body">
    <span class="step-date">DD.MM.YYYY</span>
    <span class="step-label" data-i18n="step5">Yeni mərhələ adı</span>
  </div>
</li>
```

Sonra `script.js`-də hər dil bloku üçün (`az`, `tr`, `ru`, `en`) yeni açar əlavə et:

```js
step5: "Yeni mərhələ adı",   // və hər dilə tərcüməsi
```

**Davam edən mərhələ**: `class="step ongoing"` olsun. Tarix yerinə `data-i18n="stepDateOngoing"` istifadə et — bu hər dildə "Davam edir / Devam ediyor / Продолжается / Ongoing" göstərir. Saytda eyni anda yalnız bir `ongoing` mərhələ olması məsləhətdir.

---

## 2. Meta Pixel-i necə əlavə etmək

`index.html` faylının `<head>` bölməsində bu blok var:

```html
<!-- META PIXEL PLACEHOLDER: insert pixel code here, PIXEL_ID = __________ -->
```

Aşağıda hazır kod şərh içindədir. İki addım:

1. `<!--` və `-->` şərh işarələrini sil.
2. Hər iki `PIXEL_ID_HERE` yerinə Meta Ads Manager-dən aldığın pixel ID-ni (məsələn `123456789012345`) yaz.

Pixel quraşdırıldıqdan sonra Meta Ads Manager-də "Test Events" bölməsində bu səhifəyə daxil olub PageView event-in gəlib-gəlmədiyini yoxla.

---

## 3. GitHub-a yükləmək (GitHub Pages-də deploy)

Layihə qovluğunda terminal aç:

```bash
cd "C:\Users\ceyhu\Projects\sehlaayardimet.github.io"

git init
git add .
git commit -m "Initial site"
git branch -M main

# yeni boş repo: github.com/sehlaayardimet/sehlaayardimet.github.io
# (Public seç, README/license/.gitignore əlavə etmə)

git remote add origin https://github.com/sehlaayardimet/sehlaayardimet.github.io.git
git push -u origin main
```

Push edərkən GitHub Personal Access Token (PAT) lazım olacaq — şifrə əvəzinə tokeni yapışdır.

GitHub Pages avtomatik aktiv olur, çünki repo adı `<istifadəçi>.github.io` formatındadır. 1–2 dəqiqədən sonra sayt bu ünvanda işləyəcək:

**https://sehlaayardimet.github.io**

Sonradan dəyişiklik etdikdə:
```bash
git add .
git commit -m "qısa təsvir"
git push
```

---

## 4. Sonrakı yenilikləri yerli olaraq necə yoxlamaq

Sadəcə `index.html`-i brauzerdə aç (cüt klik). Hər şey işləyəcək — heç bir server lazım deyil. Mobil görünüşü yoxlamaq üçün Chrome DevTools (`F12`) → cihaz emulyatoru → iPhone SE (375px) və ya Galaxy S8 (360px).

---

## 5. Dizayn qeydləri

- Rəng paleti: `--bg #FAFCF7`, `--green #97C459`, `--green-mid #3B6D11`, `--green-dark #173404`. Donation paneli `#173404` arxa fonludur (kontrast üçün).
- Şriftlər: heading üçün **Fraunces** (warm display serif), body üçün **Mulish** (humanist sans), kart nömrəsi üçün **JetBrains Mono**. Hamısı Google Fonts-dan yüklənir.
- Pul sayğacı / progress bar yoxdur və olmamalıdır.
- Floating WhatsApp düyməsi bütün scroll boyu sağ-alt küncdə qalır.
