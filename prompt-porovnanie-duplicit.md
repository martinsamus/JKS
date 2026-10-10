# Úloha: podrobný porovnávací report duplicitných piesní (len čítanie, nič nemeň)

## Kontext
Repozitár `C:\GitHub\JKS` je dátový repozitár: `Piesne/` obsahuje slovenské cirkevné piesne exportované z OpenLP 3.1.7 ako jeden XML súbor (OpenLyrics 0.8) na pieseň. Prečítaj si `CLAUDE.md` (formát, tagy, konvencia názvov súborov) a `duplicity.md` (zoznam skupín duplicít s odškrtnutými hotovými a otvorenými položkami).

Spracuj **všetky otvorené položky `- [ ]`** v sekciách 4a, 4c a 4d súboru `duplicity.md` (asi 59 skupín). Pri tých, kde je pri skupine poznámka „už zlúčené“, porovnávaj len súbory, ktoré v skupine reálne ešte existujú. Kontroluj existenciu súborov v `Piesne/` (v názvoch môže byť nezlomiteľná medzera U+00A0).

**Čo do porovnávania nepatrí:**
- Sady `JKS1`, `JKS2`, `JKS3` (zámerné samostatné importy). Použi ich len ako referenčný zdroj textu (pozri bod C).
- **Verzie s akordmi.** Nie je potrebné porovnávať verziu s akordmi a bez nich; môžu existovať vedľa seba. Za verziu s akordmi považuj každý súbor s tagom `akordy` alebo s ľubovoľným `<chord …/>` elementom. Takéto súbory z porovnávania **úplne vynechaj**: neporovnávaj ich text, nezaraďuj ich do tabuliek ani do zoznamov rozdielov a **nikdy neodporúčaj ich zmazať ani zlúčiť s inou verziou**. Ak je taká verzia v skupine, spomeň ju len jednou vetou („Existuje aj verzia s akordmi: …, ponechaná zámerne“) a skupinu spracuj, akoby v nej nebola. Ak po vynechaní ostane v skupine jediný súbor, skupinu uveď len ako „nie je čo porovnať“.
- Výnimka: ak má súbor bez tagu `akordy` v texte náhodný `<chord>` element (napr. text uložený omylom ako názov akordu), nejde o verziu s akordmi. Označ to ako chybu formátu a porovnaj ho normálne.

## Pravidlá (prísne)
1. **Iba čítaj.** Nemeň, nepremenúvaj ani nemaž žiadne súbory v `Piesne/`. Jediným výstupom je nový markdown súbor `duplicity-rozdiely.md` v koreni repozitára (nekomituj ho a nepushuj).
2. **Presnosť pred rýchlosťou.** Každé tvrdenie o rozdiele musí byť overené skriptom, nie odhadnuté. Cituj presný text (so slohou, riadkom a súborom). Ak si niečím nie si istý, napíš „neisté“ a čo presne treba skontrolovať. Nikdy nedomýšľaj.
3. Nepoužívaj len skóre podobnosti (pri bežných frázach vychádza podhodnotené). Rozdiely vypočítaj priamym porovnaním textov (`difflib` na slovách a riadkoch).
4. Skripty píš do scratchpad adresára, nie do projektu. Python spúšťaj ako `python -I -X utf8`. Cesty vždy v úvodzovkách (názvy majú medzery, čiarky, zátvorky, diakritiku). XML čítaj `xml.etree` len na čítanie.
5. Reportuj slovensky.
6. **Každá skupina musí mať odporúčanie a dôvod.** Odporúčanie nesmie byť všeobecné („lepšia verzia“), ale musí sa opierať o konkrétne, overené rozdiely z reportu (napr. „A má kompletné 3 slohy, B len 2; A nemá preklepy, B má 2 – ‚zmelina‘, ‚Galiley‘“). Rozhodnutie je na mne, ty len odporúčaš.

## Čo porovnať pri každej skupine
Pre každý súbor v skupine (okrem verzií s akordmi) vyextrahuj a porovnaj:

**A. Metadáta**
- `<title>` (všetky), `<author>` (tagy), `<songbooks>`, `<verseOrder>`, `<copyright>`, `<ccliNo>`.
- Názov súboru a či zodpovedá konvencii „prvý titul + (autori zoradení podľa kódov znakov)“.

**B. Štruktúra**
- Počet a názvy slôh (`v1`, `c1`, `b1`, `v1a`/`v1b`…) a ich poradie. Zhoduje sa `verseOrder` s poradím v dokumente? Chýbajúce alebo extra slohy a refrény.
- Ako je refrén uložený (samostatná `c1` sloha vs vpísaný do slôh, `R:` / `Ref.` v texte, `/: :/`, `|: :|`, `[: :]`).
- Ako je text rozdelený na `<lines>` (viac `<lines>` v jednej sloha, `break="optional"`).

**C. Text (slovo po slove)**
- Chýbajúce, pridané a zmenené slová/riadky medzi súbormi, s presnou citáciou.
- Preklepy a nedôslednosti (napr. „Galiley“, „zmelina“, „potrebujeme“, zlepené slová), chýbajúca diakritika, veľké/malé písmená, „Ty/ty“, „Tvoje/tvoje“.
- Interpunkcia, pomlčky v slabikách („mi-lý“), opakovania napísané vs označené značkou, odkazy typu „atď.“, „4x“, „3x“.
- Ak ide o text z oficiálneho JKS, porovnaj aj s verziou JKS1/JKS2/JKS3 pod rovnakým číslom (ako **referenčný** zdroj, nie ako kandidáta na zmazanie). Zaznamenaj, ktorá verzia je k nemu bližšie.

**D. Zarovnanie a formátovanie**
- Číslovanie slôh v texte (`1.`, `2.`) a značky/čísla piesne s dlhým radom medzier (`1.      …   1.`); či sú medzery zachované, či číslo zodpovedá piesni.
- Zlomy riadkov `<br/>`, prázdne riadky navyše (`<br/><br/>`), koncové medzery a lomítka, vložené HTML (`<p style="page-break-after…"/>`).
- Pokyny v texte, ktoré by sa zobrazili na slajde (`medzihra`, `vyhrávka`, `celé 3x`, `R:`, `Ofertórium:`).
- Smerové značky typu `[=>E]` a chyby formátu s `<chord>` elementmi podľa výnimky vyššie.

**E. Rozsah**
- Počet slôh, riadkov a slov v každom súbore a ktorý je najúplnejší.

## Výstup: markdown súbor `duplicity-rozdiely.md`
Report ulož ako markdown súbor `C:\GitHub\JKS\duplicity-rozdiely.md` (UTF-8, LF). Použi jednoduchý GitHub markdown (nadpisy, tabuľky, odrážky, bloky kódu na citácie), aby sa dal čítať aj v editore, nielen v prehliadači.

Na začiatku súboru:
- **Súhrnná tabuľka všetkých skupín**: číslo skupiny, súbory, typ rozdielov (formát / preklepy / chýbajúci text / rôzne verzie), **odporúčaná akcia** (zlúčiť automaticky / treba rozhodnúť / nechať obe / nie je čo porovnať) a **odporúčaný súbor na ponechanie**.
- Zoznam skupín, kde sú len formátovacie rozdiely, aby sa dali spracovať hromadne.

Potom pre každú skupinu (v poradí ako v `duplicity.md`):

1. Nadpis s názvami súborov v skupine (verzie s akordmi len ako poznámka).
2. **Zhrnutie jednou vetou** (napr. „B má navyše 3. slohu, A má lepší text slôh 1–2“).
3. **Tabuľka metadát a štruktúry** (stĺpec = súbor): tagy, tituly, verseOrder, počet slôh/riadkov/slov, zarovnanie.
4. **Zoznam rozdielov v texte**: číslovaný, každý rozdiel ako „súbor X, sloha Y, riadok Z: `…` vs `…`“ s typom (preklep / chýba slovo / chýba sloha / interpunkcia / formát / pokyn v texte).
5. **Unikátny obsah**: čo má každý súbor, čo ostatné nemajú (slohy, riadky, tagy, tituly) — to, čo by sa stratilo po zmazaní.
6. **Odporúčanie** (povinné pri každej skupine), v tomto tvare:
   - **Ponechať:** názov súboru.
   - **Zmazať / zlúčiť:** ktoré súbory (nikdy verzia s akordmi).
   - **Prečo:** 2 – 5 odrážok, každá s konkrétnym overeným argumentom z bodov 3 – 5 (úplnosť slôh, preklepy, diakritika, štruktúra refrénu, verseOrder, zhoda s referenčným JKS, pokyny v texte, zarovnanie).
   - **Čo prevziať z ostatných:** konkrétne slohy/riadky/opravy/tagy/tituly, ktoré sa majú pridať do ponechanej verzie.
   - **Istota:** vysoká / stredná / nízka, s jednou vetou prečo.
7. **Riziká a neistoty**: napr. môžu to byť rôzne melódie, nejasné, ktorý text je správny, odkazy na tlačený spevník, ktoré nevieš overiť.

## Kontrola pred odovzdaním
- Počet spracovaných skupín = počet otvorených skupín v `duplicity.md`; každá skupina má sekciu „Odporúčanie“ s vyplneným „Prečo“.
- Žiadny súbor s tagom `akordy` ani s akordmi nie je v tabuľkách, v zoznamoch rozdielov ani v odporúčaní zmazať/zlúčiť (over skriptom).
- Súbor `duplicity-rozdiely.md` existuje a otvorí sa ako platný markdown (tabuľky majú rovnaký počet stĺpcov).
- Každý súbor spomenutý v reporte existuje; každá citácia sa dá nájsť v súbore (over skriptom).
- `git status` nesmie ukázať žiadnu zmenu v `Piesne/`; nový je iba `duplicity-rozdiely.md`.
- Na konci v odpovedi uveď cestu k súboru, počet skupín podľa odporúčanej akcie a čo si nedokázal overiť.
