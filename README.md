# Krycí jména pro Michala

Sada 25 interaktivních kartiček ve formátu pivního podtácku (cca 9×9 cm). Každá kartička zobrazuje slovo na horní i spodní straně — dolní text je otočen o 180°, takže je čitelný z druhé strany stolu.

---

## Soubory

| Soubor | Popis | Velikost |
|--------|-------|----------|
| `kryci_jmena_pro_michala.html` | Hlavní verze s ilustracemi | 71 KB |
| `kryci_jmena_pro_michala_90.html` | Ilustrace s clipPath zónou (bez rotace) | 79 KB |
| `kryci_jmena_pro_michala_text.html` | Textová verze + dynamické přidávání karet | 47 KB |

---

## Kartičky (25 slov)

| # | Slovo | Poznámka |
|---|-------|----------|
| 1 | Papaya | tropické ovoce |
| 2 | Slečna | postava s šaty |
| 3 | Mustang | divoký kůň |
| 4 | Vejce | rozbité vejce se žloutkem |
| 5 | Gumicuk | upínací guma s háčky |
| 6 | Déšť | mrak s dešťovými kapkami |
| 7 | Minerálka | lahev minerální vody |
| 8 | Pošťák | poštovní doručovatel |
| 9 | Vlak | parní lokomotiva s vagónem |
| 10 | Moucha | moucha s průsvitnými křídly |
| 11 | Facka | ruka s hvězdičkovým efektem |
| 12 | Koule | tři kroketové koule (červená, žlutá, modrá) |
| 13 | Agrese | rozzuřený obličej |
| 14 | Masáž | masáž zad na lehátku |
| 15 | Potápěč | potápěč v neoprenu s bublinami |
| 16 | Letenka | palubní průkaz PRG → JFK |
| 17 | Palestinec | muž s kéfíjou |
| 18 | Prkno | surfařské prkno s ploutví |
| 19 | Brzda | kotoučová brzda s třmenem |
| 20 | Jukebox | retro jukebox s barevnými světly |
| 21 | Ručka | páka ruční brzdy s červeným tlačítkem |
| 22 | Hřebínek | panorama hřebene Jizerských hor (875 m n.m.) |
| 23 | Jiřetín | znak obce Jiřetín pod Bukovou (Buková hora + hračka DETOA) |
| 24 | Albrechtice | znak obce Albrechtice v Jizerských horách (smrky + mlýnské kolo) |
| 25 | Jablonec | znak města Jablonec nad Nisou (jabloň + pramen + hradební koruna) |

---

## Funkce

### Všechny verze
- **Matice 5×5** — 25 kartiček v pevném gridu, responzivní pro menší obrazovky
- **Shuffle** — zlaté tlačítko náhodně přeuspořádá kartičky s animací (Fisher-Yates algoritmus)
- **Zoom** — kliknutí na kartičku otevře plnorozměrný náhled přes celou obrazovku; zavření klávesou Escape nebo kliknutím

### Textová verze (`_text.html`)
- Kartičky bez ilustrací — pouze text
- Každá kartička rozdělena **pomyslnou čárou uprostřed**
  - horní polovina: béžové pozadí, slovo vycentrováno
  - dolní polovina: bílé pozadí, slovo otočeno o 180° a vycentrováno
- **Dynamické přidávání karet** — pole dole umožňuje zadat nové slovo
  - okamžitě se přidá textová kartička do matice
  - na pozadí se zavolá Claude API (`claude-sonnet-4-20250514`), který vygeneruje SVG ilustraci
  - ilustrace se automaticky vloží do středové zóny kartičky
  - počítadlo kartiček se aktualizuje

---

## Design

- **Formát:** 680 × 420 px SVG (poměr pivního podtácku)
- **Pozadí kartiček:** béžová `#FBF7EE`, zlatý rámeček `#C8A84B`, vnitřní čárkovaná linka `#E8C96A`
- **Písmo:** Georgia serif, 34–56 px, černá `#111111`
- **Tmavé pozadí stránky:** `#1a1208` se zlatými akcenty
- **Nadpis:** Playfair Display, podtitulky IM Fell English

---

## Použití

Stačí otevřít libovolný `.html` soubor v prohlížeči — žádná instalace ani server není potřeba.

Pro dynamické generování ilustrací (pouze `_text.html`) je potřeba připojení k internetu a přístup k Anthropic API.

---

## Technologie

- čisté HTML + CSS + JavaScript (žádné frameworky)
- SVG ilustrace generované ručně i přes Anthropic Claude API
- Heraldické znaky: Jiřetín pod Bukovou, Albrechtice v Jizerských horách, Jablonec nad Nisou

---

## GitHub Pages — perzistentní ukládání slov

Přidaná slova od návštěvníků se ukládají přes `window.storage` API (claude.ai artifacts storage). Při každém dalším načtení stránky se uložená slova automaticky obnoví včetně jejich ilustrací.

### Nasazení na GitHub Pages

1. Ulož soubory do repozitáře (např. `docs/` složka nebo root)
2. V Settings → Pages zvol větev a složku
3. Stránka bude dostupná na `https://<user>.github.io/<repo>/`

> **Poznámka k storage:** `window.storage` je dostupné v prostředí claude.ai. Pro samostatné GitHub Pages nasazení je potřeba nahradit storage backend — doporučené možnosti:
> - **localStorage** (data zůstanou jen v daném prohlížeči)
> - **GitHub Gist API** (sdílená data pro všechny návštěvníky, vyžaduje token)
> - **Supabase / Firebase** (plnohodnotná databáze zdarma)

### Ukázka náhrady za localStorage (nejjednodušší)

```js
// Místo window.storage.get('custom-words'):
const words = JSON.parse(localStorage.getItem('custom-words') || '[]');

// Místo window.storage.set('custom-words', JSON.stringify(words)):
localStorage.setItem('custom-words', JSON.stringify(words));
```

