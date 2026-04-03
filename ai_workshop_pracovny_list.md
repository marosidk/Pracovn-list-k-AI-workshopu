# AI Workshop - Pracovný list

### Primárne zdroje

| Zdroj | Odkaz |
| --- | --- |
| PDF dokument | **AI\_Workshop.pdf** |
| YouTube playlist | [Claude Code Workshop](https://youtube.com/playlist?list=PLJW-oHbyRDeL62yOcaqjex7cKnzcEYQXi&si=JUX_Bc2piFMk1NwJ) |
| GitHub dokumentácia | [github.com/Kames003/Claude-](https://github.com/Kames003/Claude-) |

---

## Úvod: Čo je AI Asistent?

### Architektúra

```
+-------------+     +------------------+     +-------------+
| POUZIVATEL  | <-> |   AI ASISTENT    | <-> |     LLM     |
|             |     |   (interface)    |     |   (model)   |
+-------------+     +------------------+     +-------------+
     Ty                 Prostredník            "Mozog"
```

**LLM (Large Language Model)** je samotný jazykový model - "mozog", ktorý generuje odpovede. Príklady: GPT-4, Claude, Gemini, Llama...

**AI Asistent** je vrstva medzi tebou a LLM. Je to softvér, ktorý prijíma tvoje požiadavky, pridáva kontext, posiela to do LLM, prijíma odpoveď a môže vykonávať akcie (editovať súbory, spúšťať príkazy).

---

# ČASŤ 1: Setup a základy

## 1. CLI vs GUI

**CLI** znamená **Command Line Interface** a znamená to, že s nástrojom komunikujeme cez **príkazový riadok (terminál)**.

**GUI** znamená **Graphical User Interface** - klasické okná, tlačidlá, myš.

### Výhody CLI pre programátorov

- Rýchlejšie pre skúsených používateľov
- Ľahko sa **skriptuje / automatizuje** (automatizácia)
- Funguje cez **vzdialené pripojenie** (SSH)
- Menej náročné na **systémové prostriedky (RAM, CPU)**

---

## 2. Sessions - konverzácie s AI

### Kedy začať novú session?

1. **Keď som dokončil jednu ucelenú úlohu a chcem začať pracovať na úplne inej téme, aby som predišol zmäteniu AI neaktuálnym kontextom.**
2. **Keď konverzácia narástla natoľko, že AI začína strácať prehľad o skorších častiach, alebo sa blíži limit context window.**

---

# ČASŤ 2: Base usage a IDE integrácia

## 3. Konfigurácia AI Asistentov

### Prečo existujú lokálne nastavenia?

Lokálne nastavenia typicky **nie sú** súčasťou Git repozitára.

Je to preto, lebo: **každý vývojár môže mať iné osobné preferencie, rôzne cesty k nástrojom alebo citlivé informácie (napr. API kľúče), ktoré nechce zdieľať s celým tímom cez repozitár.**

---

## 4. Context Window a Tokeny

### Compaction (komprimácia)

**Compaction** = **automatický proces, pri ktorom AI asistent zhrnie/komprimuje históriu dlhej konverzácie do kratšieho súhrnu, aby uvoľnil miesto v context window a mohol pokračovať v práci.**

**Výhoda:** AI môže pokračovať v práci

**Nevýhoda:** **Strata detailov** (niektoré detaily sa stratia)

---

## 5. IDE Integrácie

Ľahšie sa **kontrolujú a prezerajú** zmeny pred ich akceptovaním.

---

# ČASŤ 3: Advance Permissions Management

## 6. Permissions - bezpečnosť

### Čo stále vyžaduje povolenie:

- **Spúšťanie shell príkazov**
- **Git operácie (push, reset, force operácie)**
- Operácie mimo projekt

---

## 7. Dangerous Mode

**Riziká:**

- AI môže **prepísať/zmazať** git históriu
- AI môže **nenávratne zmazať** súbory
- AI môže spustiť **škodlivé alebo neočakávané** skripty

### Kedy by sa to mohlo hodiť?

Pri použití v kombinácii so **sandboxovým / izolovaným** prostredím.

---

## 8. Sandbox - izolované prostredie

Predstav si sandbox ako: **hraciu plochu z piesku, kde môžeš stavať čokoľvek – a aj keby si celú stavbu zničil, zvyšok ihriska zostane nedotknutý. Rovnako sandbox izoluje AI od zvyšku systému, takže prípadné chyby neovplyvnia produkčné dáta ani iné projekty.**

---

# ČASŤ 4: Version Control a Undo

## 9. Vracanie zmien

### Prečo je Git dôležitý pri práci s AI?

1. **AI môže urobiť zmeny vo viacerých súboroch naraz – bez Git histórie by nebolo možné jednoducho vrátiť len konkrétne zmeny späť.**
2. **Git umožňuje porovnať stav pred a po zásahu AI, čo pomáha odhaliť chyby alebo nežiaduce úpravy.**

### Dôležité

Pred väčšími zmenami je **VŽDY** dobré urobiť **git commit (alebo aspoň git stash)**.

---

# ČASŤ 5: Plan Mode

## 10. Plan Mode

### Kedy použiť Plan Mode?

- Pri **komplexných a rozsiahlych** úlohách
- Keď si **nie som istý** výsledkom
- Pri úlohách ovplyvňujúcich **viacero súborov alebo architektúru projektu**

### Výhody

1. Predídeš zbytočným **chybám a zbytočným prerobám**
2. Môžeš ovplyvniť riešenie **skôr** než je implementované
3. AI lepšie **pochopí** tvoje požiadavky

---

# ČASŤ 6: Context Engineering a projektové inštrukcie

## 11. Špecifické inštrukcie a SPEC.md

**Prečo je to lepšie?** **CLAUDE.md zostáva stručný a prehľadný. SPEC.md obsahuje detaily, ktoré AI načíta len vtedy, keď ich naozaj potrebuje – čím sa šetrí context window a AI nie je zbytočne zaťažená informáciami, ktoré aktuálne nevyužije.**

---

## 12. Projektové inštrukcie (CLAUDE.md)

Tento súbor sa **automaticky načíta** pri každej session a stáva sa súčasťou **system promptu (kontextu AI)**.

### Prečo má byť stručný?

**Pretože CLAUDE.md sa vkladá do každej session a zaberá miesto v context window. Čím je dlhší, tým menej miesta zostáva pre skutočnú prácu, históriu konverzácie a odpovede AI. Stručné pravidlá sú navyše ľahšie pochopiteľné.**

---

## 13. Context Engineering

### Základné princípy

| Princíp | Vysvetlenie |
| --- | --- |
| Relevantnosť | Pridávaj len **priamo súvisiace** informácie |
| Stručnosť | Šetri **tokeny / priestor v context window** |
| Štruktúra | Používaj formátovanie pre **lepšiu čitateľnosť a pochopenie** |

### Prečo sú XML tagy lepšie?

**XML tagy jasne ohraničujú, čo je chybová správa a čo je bežný text promptu. AI tak presne vie, ktorá časť vstupu je chyba, a nemusí hádať kontext – to vedie k presnejším a relevantnejším odpovediam.**

---

# ČASŤ 7: Nástroje a rozšírenia

## 15. Thinking Mode

| Výhody | Nevýhody |
| --- | --- |
| Vidíš ako AI uvažuje | Spotrebuje viac **tokenov** |
| Kvalitnejšie odpovede | **Pomalšia** odpoveď |
| Odhalíš chyby v uvažovaní | |

### Kedy ho vypnúť?

Pri **jednoduchých a rutinných** úlohách, kde nepotrebujeme detailné uvažovanie.

---

## 16. Práca s dokumentáciou

### Tip: Markdown dokumentácia

Väčšina dokumentácií ponúka Markdown verziu. Je lepšia, pretože:

- Menej "šumu"
- Šetrí **tokeny**
- Lepšie sa **parsuje a spracováva AI modelom**

---

## 17. MCP - Model Context Protocol

Príklad: MCP server pre dokumentáciu umožňuje AI ľahšie **vyhľadávať a pristupovať k aktuálnej dokumentácii knižníc a nástrojov bez nutnosti manuálneho copy-paste**.

---

# ČASŤ 8: Skills a Custom Commands

## 18. Skills

**Výhoda používania hotových skills:** **Nemusíš vynaliezať koleso – hotové skills sú otestované, dobre napísané a ušetria ti čas pri nastavovaní. Môžeš sa okamžite sústrediť na svoju úlohu namiesto konfigurácie.**

---

# ČASŤ 9: Hooks a Plugins

## 20. Hooks

### Príklad použitia

Po každej úprave súboru automaticky spustiť formátovač kódu.

**Hook sa spustí po:** **uložení/zapísaní súboru (PostToolUse – File Write)**

**Vykoná:** **automatické spustenie formátovača kódu (napr. Prettier alebo Black)**

---

# ČASŤ 10: Feedback Loops a Multi-Agent systémy

## 22. Feedback Loops

### Prečo je to dôležité?

AI môže robiť chyby. Feedback loop jej umožňuje:

1. Vykonať zmenu
2. **Overiť / otestovať** výsledok
3. Opraviť chyby
4. Opakovať

### Príklad: Playwright

Playwright umožňuje AI otvoriť prehliadač a **automaticky otestovať / interaktívne skontrolovať** webstránku.

**Nevýhoda feedback loops:** Vyššia spotreba **tokenov a času**

### Pozor na testy písané AI

AI má tendenciu písať testy, ktoré **vždy prechádzajú (sú navrhnuté tak, aby potvrdili správnosť kódu, nie aby odhalili chyby)**.

Preto je dobré testy buď písať pred implementáciou alebo ich **manuálne skontrolovať a prípadne prepisovať**.

---

## 23. Multi-Agent systémy (Ralph Loops)

### Výhody

- Menej manuálnej práce
- Vhodné pre **opakujúce sa alebo paralelizovateľné úlohy**

### Nevýhody

- Menšia **kontrola** nad procesom
- Agent sa môže "zaseknúť"
- Stále potrebuješ dobrý **kontext (project instructions)** a jasné úlohy

### Čo je potrebné pre úspešný Ralph Loop?

1. Dobre definované **úlohy (tasks / PRD)**
2. Funkčné **testy**
3. Sandbox prostredie pre **bezpečné spúšťanie zmien**
4. Kvalitný project **kontext / inštrukcie (CLAUDE.md)**

---

# Zhrnutie

## 24. Prehľad konceptov

| Pojem | | Definícia |
| --- | --- | --- |
| Context Window | → | **C.** Maximálna kapacita "pamäte" LLM |
| Compaction | → | **A.** Automatická kompresia konverzácie |
| Sandbox | → | **B.** Izolované bezpečné prostredie |
| Skills | → | **E.** Rozšírené schopnosti pre špecifické úlohy |
| Custom Commands | → | **D.** Znovu použiteľné prompty |
| Hooks | → | **F.** Automatické reakcie na udalosti |
| Feedback Loop | → | **G.** AI overuje svoju vlastnú prácu |
| Ralph Loop | → | **H.** Agent pracujúci v automatickej slučke |

---

## Reflexia

**Čo ťa z workshopu najviac zaujalo alebo prekvapilo?**

Najviac ma zaujala myšlienka *Context Engineering* – teda že kvalita výstupu AI nezávisí len od toho, aký model použiješ, ale najmä od toho, ako dobre mu poskytnúť kontext. Prekvapilo ma, ako veľmi môže štruktúrovaný systémový prompt (napr. CLAUDE.md) zmeniť správanie AI v celom projekte.

---

**Aké sú podľa teba najväčšie výhody používania AI asistentov?**

- **Zrýchlenie rutinných úloh** – generovanie boilerplate kódu, refaktoring, písanie testov
- **Okamžitá dostupnosť** – AI je k dispozícii kedykoľvek, nepotrebuje prestávky
- **Podpora pri učení** – AI dokáže vysvetliť neznáme koncepty priamo v kontexte projektu

---

**Aké sú podľa teba najväčšie riziká?**

- **Prílišná dôvera** – výstup AI môže obsahovať chyby alebo bezpečnostné zraniteľnosti, ktoré bez kontroly skončia v produkcii
- **Závislosť** – vývojár, ktorý sa spoľahne výlučne na AI, nemusí pochopiť, čo kód skutočne robí
- **Strata kontextu** – pri dlhých konverzáciách môže AI zabudnúť dôležité detaily a vyprodukovať nekonzistentné riešenia

---

**Ako by si mohol využiť tieto koncepty vo svojich projektoch?**

- Vytvoriť **CLAUDE.md** pre každý väčší projekt s popisom architektúry, konvencií a použitých technológií
- Pred väčšou zmenou aktivovať **Plan Mode** a odsúhlasiť plán ešte pred implementáciou
- Nastaviť **Git commit** ako povinný krok pred každým väčším zásahom AI
- Využiť **Feedback Loops** cez unit testy – nechať AI, aby si sama overila správnosť svojich zmien

---

*AI Workshop | SPSIT | Tom. Muc.*
