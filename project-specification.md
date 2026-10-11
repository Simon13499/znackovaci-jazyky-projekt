# Aurora Nexus Festival 2027 – Projektová specifikace

Aurora Nexus Festival navazuje na loňský návrh festivalového webu. Zachovává zaměření na elektronickou hudbu a digitální umění, prostředí Dolních Vítkovic a dvě festivalové scény. Nový ročník rozšíří původní web o interaktivní funkce a lepší ovládání na mobilu.

## 1. Identita festivalu

| Položka | Hodnota |
|---|---|
| Název | Aurora Nexus Festival |
| Ročník | 2. ročník (2027) |
| Lokalita | Ostrava, Dolní oblast Vítkovice, Česká republika |
| Datum konání | **11.–13. června 2027** (pátek–neděle) |
| Charakter | Třídenní multižánrový festival elektronické hudby a digitálního umění, spojující koncerty, audiovizuální tvorbu a technologie |
| Hlavní žánry / témata | Electronic, techno, house, ambient; digitální kultura a audiovizuální performance |
| Rozsah programu | 3 dny, 2 scény, 60 účinkujících a 60 vystoupení |

**Scény:** Main Stage (Dolní Vítkovice; kapacita 3 000 osob) je určena pro větší taneční vystoupení. Digital Lab (Gong, Dolní Vítkovice; kapacita 600 osob) nabízí menší a experimentálnější program. Kapacity jsou orientační údaje pro návrh festivalu.

## 2. Účel webu

Web slouží jako hlavní informační a plánovací rozhraní festivalu před jeho konáním i během něj. Jeho cílem je nabídnout aktuálně zobrazitelný program, přehled účinkujících a scén, praktické informace a možnost sestavit osobní výběr vystoupení.

**Hlavní cíle:**

1. Rychle najít relevantní vystoupení podle dne, scény a žánru.
2. Představit účinkující a zpřístupnit jejich detailní profily včetně vazby na program.
3. Umožnit návštěvníkovi vytvořit a opakovaně zobrazit vlastní festivalový plán bez registrace.
4. Zjednodušit orientaci v místě konání i na mobilním zařízení.

**Důležité uživatelské akce:** návštěvník filtruje program; otevře detail vystoupení či účinkujícího; vyhledá interpreta podle jména; přidá nebo odebere vystoupení ze svého programu; zobrazí informace o scéně a dopravě. Web zůstane použitelný i na tabletu a mobilu díky responzivnímu rozvržení a rozbalovacímu hamburger menu.

Web bude postavený na HTML, CSS a JavaScriptu. Festivalová data budeme načítat z XML. Nepočítáme s registrací, nákupem vstupenek ani synchronizací osobního programu mezi zařízeními.

## 3. Cílové skupiny

| Cílová skupina | Potřeby | Očekávání | Potřebné informace / funkce |
|---|---|---|---|
| Fanoušci elektronické hudby | Najít oblíbené interprety a související vystoupení | Rychlá orientace v line-upu | Seznam účinkujících, vyhledávání, profil a program |
| Návštěvníci plánující celý víkend | Poskládat vystoupení napříč dny a scénami | Přehledný a uchovaný výběr | Filtry programu, osobní program, časy a scény |
| Návštěvníci na místě (zejména mobilní) | Rychle zjistit, co a kde právě či později hraje | Dobrá použitelnost na menší obrazovce | Mobilní navigace, časový přehled, detail scén |
| Zájemci o digitální umění a technologie | Objevit menší či experimentální projekty | Informace o zaměření jednotlivých interpretů | Žánry, popisy účinkujících, Digital Lab |
| První návštěvníci festivalu | Naplánovat dopravu a orientaci v areálu | Jasné a srozumitelné informace | Lokalita, scény, praktické informace |

## 4. Informační architektura

### 4.1 Sitemap

```text
Aurora Nexus Festival
├── Úvodní stránka (index.html)
├── Program (program.html)
│   ├── Filtry: den / scéna / žánr
│   └── Vystoupení → detail účinkujícího / přidání do Mého programu
├── Účinkující (ucinkujici.html)
│   ├── Vyhledávání podle jména
│   └── Detail účinkujícího (artist.html?id=...; jedna dynamická šablona)
├── Můj program (muj-program.html)
│   └── Uložená vystoupení + možnost odebrání
├── Scény (sceny.html)
│   ├── Main Stage
│   └── Digital Lab
└── Praktické informace (prakticke-informace.html)
    └── Místo konání, doprava, parkování, orientace a návštěvnické rady
```

Oproti loňské verzi přibudou hlavně sekce **Můj program**, **Scény** a společná šablona pro detaily účinkujících.

### 4.2 Hlavní navigace

Desktopová navigace: **Úvod · Program · Účinkující · Můj program · Scény · Praktické informace**. Na tabletu a mobilu se navigace sbalí pod přístupné **hamburger menu** ovládané JavaScriptem. Tlačítko bude mít odpovídající popisek a atribut `aria-expanded`; menu musí jít ovládat také klávesnicí.

### 4.3 Účel částí a jejich propojení

| Část | Účel | Propojení |
|---|---|---|
| Úvod | Představuje festival, termín, místo a hlavní výzvy k akci | Odkazy na program, účinkující a informace |
| Program | Časový seznam vystoupení se souběžnými filtry dne, scény a žánru | Z každého záznamu na interpreta a do Mého programu |
| Účinkující | Vyhledat interpreta podle jména a prohlédnout nabídku | Kliknutí otevře dynamický detail |
| Detail účinkujícího | Jméno, žánr, krátké bio a jeho vystoupení | Zpět do seznamu / přechod na příslušné vystoupení v programu |
| Můj program | Osobní přehled označených vystoupení, chronologicky seřazených | Přidání z programu, odebrání v osobním přehledu |
| Scény | Představit Main Stage a Digital Lab, umístění a charakter | Odkazy na program filtrovaný podle scény |
| Praktické informace | Základní orientace, doprava, parkování a návštěvnické informace | Odkaz na scény a úvod |

**Vazby:** programová položka patří právě jednomu účinkujícímu a jedné scéně. Detail interpreta si z dat dohledá odpovídající programové položky. Můj program uchovává pouze ID vybraných vystoupení; kompletní údaje vždy znovu čte z festivalové datové základny.

## 5. Interaktivní funkce

| Funkce | Chování pro uživatele | Plánované řešení |
|---|---|---|
| Filtrování programu | Kombinace filtrů den, scéna a žánr bez obnovení stránky | JavaScript filtruje načtené položky; žánr se odvozuje z účinkujícího přes `performerId` |
| Můj festivalový program | Přidání/odebrání vystoupení; trvalý výběr v daném prohlížeči | Uložení pole ID událostí do `localStorage`; bez účtu a synchronizace |
| Detail účinkujícího | Kliknutí na kartu vede na profil interpreta | Jediná dynamická šablona s ID interpreta v URL, např. `artist.html?id=p12` |
| Vyhledávání účinkujících | Průběžné zúžení seznamu podle textu | JavaScriptové hledání bez obnovení stránky a bez rozlišování velikosti písmen |
| Responzivní hamburger menu | Otevření a zavření navigace na tabletu a mobilu | JS přepínání stavu menu + přístupné ovládání |
| Odpočet do festivalu | Zobrazení času zbývajícího do zahájení | **Volitelné rozšíření**, na úvodu; po zahájení změna na informaci, že festival probíhá / skončil |

**Doplňující pravidla:** Program se zobrazuje chronologicky. Každé vystoupení má datum, čas začátku a konce. Pokud filtr nevrátí žádný výsledek, zobrazí se srozumitelná prázdná hláška. Výběr v Mém programu je možné změnit z více stránek; zůstává jen v daném prohlížeči. Případné překryvy termínů budou pouze informativní a nemají bránit přidání vystoupení.

## 6. Klíčové uživatelské scénáře

Tyto tři scénáře využijeme při návrhu, tvorbě i testování webu.

### S1 – Vyhledání vystoupení ve festivalovém programu

- **Typ uživatele:** návštěvník plánující návštěvu festivalu.
- **Cíl:** najít sobotní techno vystoupení na Main Stage.
- **Výchozí situace:** uživatel otevře stránku Program, která standardně ukazuje kompletní rozpis.
- **Postup:** nastaví den „sobota“, scénu „Main Stage“ a žánr „techno“.
- **Očekávaný výsledek:** bez obnovení stránky vidí pouze položky splňující všechny tři podmínky, s časy, jmény účinkujících a odkazy na jejich detaily; filtry může libovolně zrušit.
- **Ověření:** zobrazují se jen odpovídající vystoupení; po zrušení filtrů se objeví celý program.

### S2 – Sestavení osobního festivalového programu

- **Typ uživatele:** návštěvník, který si chce naplánovat několik koncertů.
- **Cíl:** uložit si vybraná vystoupení a později se k výběru vrátit.
- **Výchozí situace:** návštěvník prochází Program a zatím nemá žádné uložené vystoupení.
- **Postup:** označí dvě vystoupení pomocí tlačítka „Přidat do mého programu“, otevře Můj program, jedno vystoupení odebere a obnoví stránku.
- **Očekávaný výsledek:** zbývající vystoupení se zachová, zobrazí se správný čas a scéna a odebraná položka už v seznamu není.
- **Ověření:** seznam se aktualizuje bez obnovení stránky, nevytváří duplicity a výběr zůstane uložený.

### S3 – Nalezení účinkujícího a jeho vystoupení

- **Typ uživatele:** fanoušek konkrétního interpreta, přistupující z mobilu.
- **Cíl:** najít interpreta a zjistit, kdy a kde vystupuje.
- **Výchozí situace:** uživatel otevře web na telefonu a navigace je sbalená.
- **Postup:** otevře hamburger menu, zvolí Účinkující, zadá část jména do vyhledávání a klikne na odpovídající kartu.
- **Očekávaný výsledek:** zobrazí se správný dynamický profil s žánrem, biografií a odkazem na datum, čas a scénu daného vystoupení.
- **Ověření:** hledání funguje bez obnovení stránky, otevře se správný profil a mobilní menu jde bez problému otevřít i zavřít.

### Doplňkový scénář – Orientace mezi scénami

První návštěvník si na stránce Scény přečte rozdíl mezi Main Stage a Digital Lab, přejde do programu filtrovaného podle vybrané scény a v Praktických informacích najde základní informace o dopravě. Tento scénář je podpůrný, mimo tři hlavní testované scénáře.
