# Podrobný porovnávací report duplicitných piesní

Stav k 10. 10. 2026. Report vznikol čisto čítaním súborov v `Piesne/` (žiadny súbor v `Piesne/` sa nemenil) podľa zadania z `prompt-porovnanie-duplicit.md`. Spracované sú **všetky otvorené položky `- [ ]` zo sekcií 4a, 4c a 4d** súboru `duplicity.md`: **56 skupín** (4a: 10, 4c: 40, 4d: 6; zadanie odhadovalo ~59, v `duplicity.md` je otvorených presne 56). V skupine sú porovnávané len súbory, ktoré v `Piesne/` reálne existujú; kópie, o ktorých `duplicity.md` hovorí „už zlúčené“, už neexistujú a nie sú v porovnaní.

**Čo sa nepočíta do porovnania:** sady `JKS1`/`JKS2`/`JKS3` (použité len ako referencia textu) a **verzie s akordmi** (tag `akordy` alebo ľubovoľný `<chord …/>`). Ak má skupina verziu s akordmi, je to uvedené jednou vetou a skupina sa spracúva, akoby v nej nebola; žiadna verzia s akordmi nie je navrhnutá na zmazanie ani zlúčenie. Výnimka: súbor `Duchu Svätý, príď z neba (detsky zbor).xml` (skupina 3) nemá tag `akordy` a jeho jediný `<chord>` obsahuje omylom text piesne – posudzuje sa ako chyba formátu a porovnáva sa normálne.

## Ako čítať tabuľky a zoznamy rozdielov

- **Rozdiely v texte** sa počítajú slovo po slove (`difflib` na slovách po zložení diakritiky, veľkosti písmen a interpunkcie, bez čísel slôh na začiatku/konci riadku). Rozdiely, ktoré sú len v zápise (diakritika, veľké/malé písmená, interpunkcia, značky opakovania `[: :]`/`/: :/`/`|: :|`), sú uvedené osobitne ako „len v zápise“. Poloha = názov slohy a číslo riadku v rámci slohy (riadky sa čítajú naprieč `<lines>` blokmi).
- **Početnosť slov bez ohľadu na poradie** je kontrola nezávislá od poradia slôh: ak je „viac v A: –; viac v B: –“, majú súbory presne tie isté slová v rovnakom počte a líšia sa len poradím/štruktúrou.
- **V poradí hrania** = porovnanie po rozbalení `verseOrder` (tam, kde ho súbor má); súbory bez `verseOrder` hrajú slohy v poradí dokumentu.
- **Referencia JKS1/2/3**: pri číslovaných piesňach sa každý súbor porovnáva s importom pod rovnakým číslom; „rozdiel N“ = počet slov, ktoré sa v spoločnom zarovnaní nezhodujú; pri jednotlivých rozdieloch značka `✓`/`✗` hovorí, či daná podoba slova v referencii existuje (`✓`) alebo nie (`✗`).
- Odporúčania sú **návrhy**; rozhodnutie je na tebe. „Zlúčiť automaticky“ = odporúčaný súbor je jednoznačný a prevzatie je mechanické (tagy/titul/oprava preklepu/doplnenie slohy) bez posudzovania, ktorá verzia textu je správna. „Treba rozhodnúť“ = ostáva otvorená obsahová otázka (iné slovo, iná štruktúra alebo poradie hrania, ktoré sa z dát nedá overiť). „Nechať obe“ = rozdiel je pravdepodobne zámerný alebo môže ísť o iný nápev.

## Súhrnná tabuľka všetkých skupín

| # | Sekcia | Súbory | Typ rozdielov | Odporúčaná akcia | Odporúčaný súbor na ponechanie |
|---|---|---|---|---|---|
| [1](#g1) | 4a | A: `066. Ó, chýr preblahý (JKS, Vianočná).xml`<br>B: `O chyr Preblahy (detsky zbor).xml` | formát, preklepy | zlúčiť automaticky | `066. Ó, chýr preblahý (JKS, Vianočná).xml` |
| [2](#g2) | 4a | A: `209. Obeť svoju veľkonočnú (JKS, Veľkonočná, detsky zbor).xml`<br>B: `209. Obeť svoju veľkonočnú (bez čísel) (JKS, Veľkonočná).xml` | formát, rôzne verzie | nechať obe | `209. Obeť svoju veľkonočnú (JKS, Veľkonočná, detsky zbor).xml` + `209. Obeť svoju veľkonočnú (bez čísel) (JKS, Veľkonočná).xml` |
| [3](#g3) | 4a | A: `217. (Duch svätý, JKS).xml`<br>B: `Duchu Svätý, príď z neba (detsky zbor).xml` | formát, chýbajúci text, chyba formátu | zlúčiť automaticky | `217. (Duch svätý, JKS).xml` |
| [4](#g4) | 4a | A: `244. K stolu božej láskavosti (JKS, Začiatok).xml`<br>B: `244 jks (detsky zbor).xml` | formát | zlúčiť automaticky | `244. K stolu božej láskavosti (JKS, Začiatok).xml` |
| [5](#g5) | 4a | A: `039. Búvaj, Dieťa krásne (JKS, Vianočná).xml`<br>B: `Buvaj dieta krasne A-dur jednoduchy (detsky zbor).xml` | formát, preklepy | zlúčiť automaticky | `039. Búvaj, Dieťa krásne (JKS, Vianočná).xml` |
| [6](#g6) | 4a | A: `295. Vitaj, milý Jezu Kriste (Eucharistické, JKS).xml`<br>B: `JKS Vitaj milý Jezu (detsky zbor).xml` | formát, chýbajúci text | zlúčiť automaticky | `295. Vitaj, milý Jezu Kriste (Eucharistické, JKS).xml` |
| [7](#g7) | 4a | A: `484. Yzopom ma pokrop Pane (JKS).xml`<br>B: `Yzopom (detsky zbor).xml` | chýbajúci text, formát | zlúčiť automaticky | `484. Yzopom ma pokrop Pane (JKS).xml` |
| [8](#g8) | 4a | A: `365 (JKS).xml`<br>B: `365 Pod tvoj plášť sa utiekame, (JKS).xml` | chýbajúci text, formát | zlúčiť automaticky | `365 (JKS).xml` |
| [9](#g9) | 4a | A: `419. K tebe prichádzame (JKS).xml`<br>B: `JKS 419 - K tebe prichádzame (JKS).xml` | chýbajúci text, formát | zlúčiť automaticky | `419. K tebe prichádzame (JKS).xml` |
| [10](#g10) | 4a | A: `536. Ctime túto sviatosť slávnu (JKS).xml`<br>B: `JKS 536 - Ctíme túto sviatosť slávnu (JKS).xml` | formát, rôzne verzie | treba rozhodnúť | `536. Ctime túto sviatosť slávnu (JKS).xml` |
| [11](#g11) | 4c | A: `Boh je láska (...).xml`<br>B: `Boh je láska (Author Unknown).xml` | formát, preklepy, chyba formátu | treba rozhodnúť | `Boh je láska (...).xml` |
| [12](#g12) | 4c | A: `Bože Otče, teraz vidím (Anonymous).xml`<br>B: `Bože Otče, teraz vidím (Chvály).xml` | formát | zlúčiť automaticky | `Bože Otče, teraz vidím (Anonymous).xml` |
| [13](#g13) | 4c | A: `Čakajú ťa nástrahy (Mariánska).xml`<br>B: `Čakajú ťa nástrahy (Anonymous).xml`<br>C: `Cakaju ta nastrahy (detsky zbor).xml` | formát, rôzne verzie | zlúčiť automaticky | `Čakajú ťa nástrahy (Anonymous).xml` |
| [14](#g14) | 4c | A: `Chválim ťa, Ježiš (Chvály, Večeradlo s Pannou Máriou).xml`<br>B: `Chvalim Ta Jezis (detsky zbor).xml` | formát, rôzne verzie | treba rozhodnúť | `Chválim ťa, Ježiš (Chvály, Večeradlo s Pannou Máriou).xml` |
| [15](#g15) | 4c | A: `Dávam všetko (Adorácia, Obetné dary, Rieka života).xml`<br>B: `Dávam všetko (...).xml`<br>C: `Dnes chcel by som ti dať (Rieka Života).xml`<br>D: `Dnes chcel by som Ti dat (detsky zbor).xml` | formát, preklepy, rôzne verzie | treba rozhodnúť | `Dávam všetko (...).xml` |
| [16](#g16) | 4c | A: `Do tmy našich dní (Advent, Pomalá, Pôstna, Taize).xml`<br>B: `Do tmy našich dní (Taize).xml` | chýbajúci text | zlúčiť automaticky | `Do tmy našich dní (Advent, Pomalá, Pôstna, Taize).xml` |
| [17](#g17) | 4c | A: `Dobrorečíme Ti (Obetné dary).xml`<br>B: `Dobrorecime Ti (detsky zbor).xml` | formát, preklepy | zlúčiť automaticky | `Dobrorecime Ti (detsky zbor).xml` |
| [18](#g18) | 4c | A: `Glória - UPC (Glória).xml`<br>B: `Gloria_Vinbarg (detsky zbor).xml` | formát, preklepy | zlúčiť automaticky | `Glória - UPC (Glória).xml` |
| [19](#g19) | 4c | A: `Jasaj v Pánovi celá Zem (Veľkonočná).xml`<br>B: `Jasaj v Pánovi (Anonymous).xml` | rôzne verzie, formát | treba rozhodnúť | `Jasaj v Pánovi celá Zem (Veľkonočná).xml` |
| [20](#g20) | 4c | A: `Ježiš môj (Anonymous).xml`<br>B: `Jezis moj, pred tvojou stojim obetou (detsky zbor).xml` | formát, preklepy | zlúčiť automaticky | `Jezis moj, pred tvojou stojim obetou (detsky zbor).xml` |
| [21](#g21) | 4c | A: `Ježiš, ty si skalou (Prijímanie).xml`<br>B: `Ježiš, ty si skalou (Anonymous).xml`<br>C: `Jezis ty si skalou (detsky zbor).xml` | formát | zlúčiť automaticky | `Ježiš, ty si skalou (Prijímanie).xml` |
| [22](#g22) | 4c | A: `Kríž je znakom spásy (Pôstna, krížová cesta).xml`<br>B: `Kríž je znakom spásy (Anonymous).xml`<br>C: `Kriz je znakom spasy (detsky zbor).xml` | formát, rôzne verzie | zlúčiť automaticky | `Kríž je znakom spásy (Pôstna, krížová cesta).xml` |
| [23](#g23) | 4c | A: `Môj Boh, vďaka tebe dýcham (Prijímanie).xml`<br>B: `moj boh (detsky zbor).xml` | preklepy, chýbajúci text | zlúčiť automaticky | `Môj Boh, vďaka tebe dýcham (Prijímanie).xml` |
| [24](#g24) | 4c | A: `Taky Velky Taky maly (detsky zbor).xml`<br>B: `Môžeš svätým byť (Večeradlo s Pannou Máriou).xml` | chýbajúci text, formát | zlúčiť automaticky | `Taky Velky Taky maly (detsky zbor).xml` |
| [25](#g25) | 4c | A: `Nebojim sa (Author Unknown).xml`<br>B: `Nebojim sa (detsky zbor).xml` | preklepy | zlúčiť automaticky | `Nebojim sa (detsky zbor).xml` |
| [26](#g26) | 4c | A: `Nech vás požehnáva Pán (Author Unknown).xml`<br>B: `nech vas pozehnava pan (detsky zbor).xml`<br>C: `Požehnanie sv.Františka (Jerichove Trúby, svadobná).xml` | formát, chýbajúci text, rôzne verzie | zlúčiť automaticky | `Nech vás požehnáva Pán (Author Unknown).xml` |
| [27](#g27) | 4c | A: `NEPOŠKVRNENÉ SRDCE MÁRIE (Mariánska, Veceradlo).xml`<br>B: `Neposkvrnene Srdce Marie (detsky zbor).xml` | formát | treba rozhodnúť | `NEPOŠKVRNENÉ SRDCE MÁRIE (Mariánska, Veceradlo).xml` |
| [28](#g28) | 4c | A: `Nežne zlomený (...).xml`<br>B: `Ku krížu dvíham zrak - Nežne zlomený (Rieka Života).xml` | chýbajúci text, formát | zlúčiť automaticky | `Nežne zlomený (...).xml` |
| [29](#g29) | 4c | A: `Ty mi dávaš nohy jeleníc (Anonymous).xml`<br>B: `Nohy jeleníc (Prijímanie).xml` | rôzne verzie, formát | treba rozhodnúť | `Ty mi dávaš nohy jeleníc (Anonymous).xml` |
| [30](#g30) | 4c | A: `Otváram srdce (MaranaTha).xml`<br>B: `Otváram srdce (...).xml`<br>C: `Srdce dokorán (Anonymous).xml` | rôzne verzie, formát | treba rozhodnúť | `Otváram srdce (MaranaTha).xml` |
| [31](#g31) | 4c | A: `Pane, som tak veľmi rád (Veľkonočná).xml`<br>B: `Pane, som tak veľmi rád (Anonymous).xml` | formát, preklepy | zlúčiť automaticky | `Pane, som tak veľmi rád (Veľkonočná).xml` |
| [32](#g32) | 4c | A: `Poď, teraz je čas (Začiatok).xml`<br>B: `Pod, teraz je cas vzdat chvalu (detsky zbor).xml` | formát | zlúčiť automaticky | `Poď, teraz je čas (Začiatok).xml` |
| [33](#g33) | 4c | A: `Poďme všetci spolu (Rieka Života).xml`<br>B: `podme vsetci spolu (detský zbor).xml`<br>C: `podme chvalit ho (Anonymous).xml` | rôzne verzie, formát | treba rozhodnúť | `Poďme všetci spolu (Rieka Života).xml` |
| [34](#g34) | 4c | A: `Prijmi tieto naše dary, Pane (Obetné dary).xml`<br>B: `Príjmi tieto naše dary (detsky zbor).xml` | chýbajúci text, rôzne verzie | treba rozhodnúť | `Prijmi tieto naše dary, Pane (Obetné dary).xml` |
| [35](#g35) | 4c | A: `Si môj Pán, Ježiš Kráľ (Author Unknown).xml`<br>B: `si moj pan (Author Unknown).xml` | preklepy, formát | zlúčiť automaticky | `Si môj Pán, Ježiš Kráľ (Author Unknown).xml` |
| [36](#g36) | 4c | A: `Stretol ma dnes Pán (Prijímanie, Veľkonočná).xml`<br>B: `Tak všetci spolu chváľme ho (detsky zbor).xml` | formát, chýbajúci text | treba rozhodnúť | `Tak všetci spolu chváľme ho (detsky zbor).xml` |
| [37](#g37) | 4c | A: `Svätý (Večeradlo s Pannou Máriou).xml`<br>B: `Svaty - Pane Boze svetov nekonecnych (detsky zbor).xml` | rôzne verzie, formát | treba rozhodnúť | `Svätý (Večeradlo s Pannou Máriou).xml` |
| [38](#g38) | 4c | A: `Svoj pokoj (...).xml`<br>B: `Svoj pokoj (Anonymous).xml` | preklepy, chýbajúci text | zlúčiť automaticky | `Svoj pokoj (...).xml` |
| [39](#g39) | 4c | A: `Šťastie (Mariánska).xml`<br>B: `Je dnes taký zvláštne krásny deň (Mariánska).xml` | chýbajúci text, preklepy, rôzne verzie | treba rozhodnúť | `Šťastie (Mariánska).xml` |
| [40](#g40) | 4c | A: `Túžim priniesť na oltár (Richard Čanaky).xml`<br>B: `Obeta srdca (Obetné dary).xml`<br>C: `tuzim priniest (detsky zbor).xml` | formát, rôzne verzie | zlúčiť automaticky | `Túžim priniesť na oltár (Richard Čanaky).xml` |
| [41](#g41) | 4c | A: `Ty si Najvyšší, Ty si Pán (Author Unknown).xml`<br>B: `Ty si najvyssi (detsky zbor).xml` | preklepy, formát | zlúčiť automaticky | `Ty si Najvyšší, Ty si Pán (Author Unknown).xml` |
| [42](#g42) | 4c | A: `Ty si mojou láskou (detsky zbor).xml`<br>B: `Ty si mojou láskou (Anonymous).xml` | preklepy, formát | zlúčiť automaticky | `Ty si mojou láskou (detsky zbor).xml` |
| [43](#g43) | 4c | A: `Ty si Pánom, Ty si Kráľom (Prijímanie).xml`<br>B: `Ty si Pánom (...).xml`<br>C: `Ty si panom, ty si kralom (detsky zbor).xml` | chýbajúci text, rôzne verzie, formát | treba rozhodnúť | `Ty si Pánom, Ty si Kráľom (Prijímanie).xml` |
| [44](#g44) | 4c | A: `Vládca (MaranaTha).xml`<br>B: `Vladca (detsky zbor).xml` | formát, rôzne verzie | zlúčiť automaticky | `Vládca (MaranaTha).xml` |
| [45](#g45) | 4c | A: `Všade tam kde sú (detsky zbor).xml`<br>B: `Všade tam kde sú (Anonymous).xml`<br>C: `Privítajme Pána (Začiatok).xml` | preklepy, formát | zlúčiť automaticky | `Všade tam kde sú (detsky zbor).xml` |
| [46](#g46) | 4c | A: `Vždy je s nami tá (Mariánska).xml`<br>B: `Vždy je s nami tá (Anonymous).xml` | formát | zlúčiť automaticky | `Vždy je s nami tá (Mariánska).xml` |
| [47](#g47) | 4c | A: `ZÁCHRANÁR (Večeradlo s Pannou Máriou).xml`<br>B: `Zachranar (detsky zbor).xml` | formát, rôzne verzie | treba rozhodnúť | `Zachranar (detsky zbor).xml` |
| [48](#g48) | 4c | A: `Zvelebený Pán (Rieka Života).xml`<br>B: `Zvelebený buď (detsky zbor).xml` | formát, rôzne verzie | treba rozhodnúť | `Zvelebený Pán (Rieka Života).xml` |
| [49](#g49) | 4c | A: `Žalm 131 (Anonymous).xml`<br>B: `Nasytene dieta - Zalm 131 (detsky zbor).xml` | formát | zlúčiť automaticky | `Nasytene dieta - Zalm 131 (detsky zbor).xml` |
| [50](#g50) | 4c | A: `ŽALM (Večeradlo s Pannou Máriou).xml`<br>B: `spievaj panovi (detsky zbor).xml` | formát | zlúčiť automaticky | `ŽALM (Večeradlo s Pannou Máriou).xml` |
| [51](#g51) | 4d | A: `Pane, zmiluj sa nad nami (Kyrie).xml`<br>B: `Pane zmiluj sa nad nami (Anonymous).xml` | chýbajúci text, rôzne verzie | treba rozhodnúť | `Pane, zmiluj sa nad nami (Kyrie).xml` |
| [52](#g52) | 4d | A: `Svätý, svätý (Svätý).xml`<br>B: `Svätý,  svätý (Anonymous).xml` | rôzne verzie, preklepy | nechať obe | `Svätý, svätý (Svätý).xml` + `Svätý,  svätý (Anonymous).xml` |
| [53](#g53) | 4d | A: `Otče náš (Otče náš).xml`<br>B: `Otče náš (Večeradlo s Pannou Máriou).xml`<br>C: `Otce nas (detsky zbor).xml` | formát, preklepy | treba rozhodnúť | `Otče náš (Otče náš).xml` |
| [54](#g54) | 4d | A: `Spievaný desiatok (Večeradlo s Pannou Máriou).xml`<br>B: `Zdravas Mária (detsky zbor).xml` | formát, rôzne verzie | treba rozhodnúť | `Zdravas Mária (detsky zbor).xml` |
| [55](#g55) | 4d | A: `217. (Duch svätý, JKS).xml`<br>B: `Pieseň k Duchu Svätému (Večeradlo s Pannou Máriou).xml` | chýbajúci text, formát | zlúčiť automaticky | `217. (Duch svätý, JKS).xml` |
| [56](#g56) | 4d | A: `Keď sa raz Pán navráti k nám (Veľkonočná).xml`<br>B: `Keď sa raz Pán ... short (Prijímanie).xml` | rôzne verzie | nechať obe | `Keď sa raz Pán navráti k nám (Veľkonočná).xml` + `Keď sa raz Pán ... short (Prijímanie).xml` |

**Počet skupín podľa odporúčanej akcie:**

- **zlúčiť automaticky: 34** – 1, 3, 4, 5, 6, 7, 8, 9, 12, 13, 16, 17, 18, 20, 21, 22, 23, 24, 25, 26, 28, 31, 32, 35, 38, 40, 41, 42, 44, 45, 46, 49, 50, 55
- **treba rozhodnúť: 19** – 10, 11, 14, 15, 19, 27, 29, 30, 33, 34, 36, 37, 39, 43, 47, 48, 51, 53, 54
- **nechať obe: 3** – 2, 52, 56
- **nie je čo porovnať: 0** – –

## Skupiny, kde sú len formátové rozdiely a preklepy (vhodné na hromadné spracovanie)

Skupiny, v ktorých sa súbory líšia iba formátom (zápis opakovania, delenie riadkov, pokyny v texte, diakritika v titule) a jednotlivými preklepmi – bez chýbajúcej slohy alebo riadka textu: **1, 4, 5, 11, 12, 17, 18, 20, 21, 25, 27, 31, 32, 35, 41, 42, 45, 46, 49, 50, 53**.

Z toho s odporúčaním „zlúčiť automaticky“ (dá sa spracovať hromadne): **1, 4, 5, 12, 17, 18, 20, 21, 25, 31, 32, 35, 41, 42, 45, 46, 49, 50**. Zvyšné z tohto zoznamu (**11, 27, 53**) majú pri formáte ešte jednu otvorenú otázku (jedno slovo alebo rozsah opakovaní), pozri ich sekcie.

Skupiny, kde chýba sloha/riadok alebo sa líši poradie/znenie (nejde o čistý formát): **2, 3, 6, 7, 8, 9, 10, 13, 14, 15, 16, 19, 22, 23, 24, 26, 28, 29, 30, 33, 34, 36, 37, 38, 39, 40, 43, 44, 47, 48, 51, 52, 54, 55, 56**.

## Nálezy mimo jednotlivých skupín (zistené počas porovnania)

- **Nezlomiteľné medzery (U+00A0) v názvoch súborov** pri súboroch v porovnaní: G13 A: `Čakajú ťa nástrahy (Mariánska).xml`; G22 A: `Kríž je znakom spásy (Pôstna, krížová cesta).xml`; G32 A: `Poď, teraz je čas (Začiatok).xml`; G34 A: `Prijmi tieto naše dary, Pane (Obetné dary).xml`; G45 C: `Privítajme Pána (Začiatok).xml`. Pri navrhnutom zlúčení (G13, G22, G32, G34, G45) sa to vyrieši aj tak, ak sa ponechá/premenuje súbor bez NBSP; pri G22, G32 a G34 je ponechaný súbor s NBSP, preto treba názov a titul opraviť.
- **Rôzne zápisy tagu**: `Rieka Života` (7 súborov v `Piesne/`) vs `Rieka života` (1 súbor: skupina 15, A); `detský zbor` (skupina 33, B; ostatné používajú `detsky zbor`); `Veceradlo` bez diakritiky (skupina 27, A) popri `Večeradlo s Pannou Máriou`.
- **Chyba formátu `<chord>`**: v skupine 3 má `Duchu Svätý, príď z neba (detsky zbor).xml` text `žiaru svetla pravého.:` uložený ako názov akordu; navrhnuté zmazanie tento súbor odstráni.
- **Číslo slohy zlepené so slovom** (`1Duchu`, `2Príď`, …): skupina 3 (B), skupina 48 (B: `1.Zvelebený`).
- **Znak `"` v texte**: skupina 11 (B) obsahuje 32 úvodzoviek v druhom riadku.
- **Znak U+02BC (modifikátor apostrof)**: skupina 54 (B: `Zdravasʼ`).

<a id="g1"></a>
## G1 · [4a] `066. Ó, chýr preblahý (JKS, Vianočná).xml` · `O chyr Preblahy (detsky zbor).xml`

**Zhrnutie:** Rovnaký text; A (JKS rozloženie) má jeden preklep `beltemskom,`, B má správne `betlémskom,`, ale zlepené `sa,aby` a iný rozsah opakovaní.

**Súbory v skupine:**
- **A** = `066. Ó, chýr preblahý (JKS, Vianočná).xml`
- **B** = `O chyr Preblahy (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `066. Ó, chýr preblahý` | `O chyr Preblahy` |
| Tagy (`<author>`) | `Vianočná`, `JKS` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | `v1 v2 v3 v4` |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4` | `v1 v2 v3 v4` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 4 / 4 |
| Počet riadkov (neprázdnych) | 22 (22) | 12 (12) |
| Počet slov (bez čísel slôh) | 84 | 83 |
| verseOrder vs dokument | – | zhoduje sa s dokumentom |
| Slov po rozbalení verseOrder | 84 | 83 |
| Riadky s číslom slohy na začiatku (`1.`) | 4 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 4 | 0 |
| Riadky s dlhým radom medzier (3+) | 4 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 8 | 16 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 84 slov v A, 83 slov v B; 2 miest s rozdielom obsahu
1. [preklep / zmena slova] A v3 r.2: `beltemskom,`  vs  B v3 r.1: `betlémskom,`  [JKS1/2/3 obsahujú podobu A: JKS1✗ JKS2✗ JKS3✗; podobu B: JKS1✓ JKS2✓ JKS3✓]
     - riadok v A: `/:V kraji beltemskom,`
     - riadok v B: `[:V kraji betlémskom, v lone panenskom.:]`
2. [preklep / zmena slova] A v4 r.3–4: `sa, aby`  vs  B v4 r.2: `sa,aby`  [JKS1/2/3 obsahujú podobu A: JKS1✓ JKS2✓ JKS3✓; podobu B: JKS1✗ JKS2✗ JKS3✗]
     - riadok v A: `nám podobným tvorom stal sa,`
     - riadok v B: `[:nám podobným tvorom stal sa,aby za nás v obeť dal sa.`
   - Rozdiely len v zápise (rovnaké slová): značky opakovania: 12, interpunkcia: 5
     - značky opakovania: A v1 r.2 `/:Ó,` vs B v1 r.1 `[:Ó,`; A v1 r.4 `Zasľúbený` vs B v1 r.2 `[:Zasľúbený`; A v1 r.6 `predrahý!` vs B v1 r.3 `predrahý!:]`; A v2 r.2 `/:Zvuky` vs B v2 r.1 `[:Zvuky`; A v2 r.5 `predrahý!` vs B v2 r.3 `predrahý!:]`; A v3 r.2 `/:V` vs B v3 r.1 `[:V`; A v3 r.4 `Syn` vs B v3 r.2 `[:Syn`; A v3 r.6 `predrahý!` vs B v3 r.3 `predrahý!:]` … (+4)
     - interpunkcia: A v1 r.3 `predrahý!:/` vs B v1 r.1 `predrahý:]`; A v1 r.4 `svetu` vs B v1 r.2 `svetu,`; A v2 r.2 `anjelské:/` vs B v2 r.1 `anjelské,:]`; A v2 r.3 `hlásia,` vs B v2 r.2 `[:hlásia`; A v3 r.3 `panenskom:/` vs B v3 r.1 `panenskom.:]`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `aby`×1, `beltemskom,`×1, `sa`×1; viac v B: `betlémskom,`×1, `sa,aby`×1
   - V poradí hrania (po rozbalení verseOrder): 84 vs 83 slov, 2 miest s rozdielom obsahu: A `beltemskom,` vs B `betlémskom,`; A `sa, aby` vs B `sa,aby`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `JKS`, `Vianočná` · tituly: `066. Ó, chýr preblahý` · text (slová, ktoré v žiadnom inom súbore nie sú): v3 r.2: `beltemskom,`; v4 r.3–4: `sa, aby`
- **B**: tagy: `detsky zbor` · tituly: `O chyr Preblahy` · verseOrder `v1 v2 v3 v4` · text (slová, ktoré v žiadnom inom súbore nie sú): v3 r.1: `betlémskom,`; v4 r.2: `sa,aby`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3, len referencia)**

| Referencia | A | B |
|---|---|---|
| `066. Ó chýr preblahý (JKS1).xml` (84 slov, slohy: v1 v2 v3 v4) | 84 slov, rozdiel 1 (zhoda 99 %) | 83 slov, rozdiel 2 (zhoda 98 %) |
| `066. Ó, chýr preblahý (JKS2).xml` (83 slov, slohy: v1 v2 v3 v4) | 84 slov, rozdiel 3 (zhoda 96 %) | 83 slov, rozdiel 3 (zhoda 96 %) |
| `066. Ó, chýr preblahý (JKS3).xml` (84 slov, slohy: v1 v2 v3 v4) | 84 slov, rozdiel 1 (zhoda 99 %) | 83 slov, rozdiel 2 (zhoda 98 %) |

**Odporúčanie**

- **Ponechať:** `066. Ó, chýr preblahý (JKS, Vianočná).xml` (A)
- **Zmazať / zlúčiť:** `O chyr Preblahy (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Slovný obsah je rovnaký, líši sa len 2 miestami: `beltemskom,` (A, v3 r.2) vs `betlémskom,` (B, v3 r.1) a `sa, aby` (A, v4 r.3–4) vs `sa,aby` (B, v4 r.2). Všetky tri referencie (JKS1, JKS2, JKS3) majú podobu „betlemskom/betlémskom“ a „sa, aby“.
  - A má JKS rozloženie (číslo slohy `1.` + koncová značka `66.` pri všetkých 4 slohách) a kratšie riadky (22 riadkov oproti 12 v B, kde sú riadky zlepené do jedného dlhého).
  - Rozsah opakovania v A (`/:Ó, chýr preblahý,` … `ó, čas predrahý!:/`, teda len prvé dva riadky) zodpovedá referenciám JKS1/JKS2/JKS3, kde sa opakovanie končí za `ó, čas predrahý!`; B opakuje aj druhý blok (`[:Zasľúbený dávno svetu, Vykupiteľ, hľa, už je tu.` … `Ó, chýr preblahý, ó, čas predrahý!:]`).
  - B nemá nič, čo by A nemalo: `verseOrder` `v1 v2 v3 v4` je totožný s poradím v dokumente.
- **Čo prevziať z ostatných:**
  - V A opraviť `beltemskom` → `betlémskom`.
  - Do A pridať tag `detsky zbor` (pôvodný súbor «066. Ó, chýr preblahý (JKS, Vianočná, detsky zbor).xml»).
- **Istota:** vysoká – Rozdiel je len jeden preklep v A a formát; správne podoby potvrdzujú všetky tri referencie.

**Riziká a neistoty:**

- Rozsah opakovania `[: :]` v B môže odrážať vlastnú prax detského zboru; nedá sa overiť bez tlačeného spevníka.

---

<a id="g2"></a>
## G2 · [4a] `209. Obeť svoju veľkonočnú (JKS, Veľkonočná, detsky zbor).xml` · `209. Obeť svoju veľkonočnú (bez čísel) (JKS, Veľkonočná).xml`

*Poznámka: `duplicity.md` uvádza pri tejto skupine aj kópie, ktoré už neexistujú (už zlúčené); porovnávané sú len súbory uvedené vyššie.*

**Zhrnutie:** Text je rovnaký až na jedno slovo (`Galileje,` vs `Galiley,`) a úvodzovky »…«; B je zjavne zámerná variant bez čísel slôh (má to v názve).

**Súbory v skupine:**
- **A** = `209. Obeť svoju veľkonočnú (JKS, Veľkonočná, detsky zbor).xml`
- **B** = `209. Obeť svoju veľkonočnú (bez čísel) (JKS, Veľkonočná).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `209. Obeť svoju veľkonočnú` | `209. Obeť svoju veľkonočnú (bez čísel)` |
| Tagy (`<author>`) | `JKS`, `Veľkonočná`, `detsky zbor` | `JKS`, `Veľkonočná` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4 v5 v6 v7` | `v1 v2 v3 v4 v5 v6 v7` |
| Počet slôh / `<lines>` blokov | 7 / 7 | 7 / 7 |
| Počet riadkov (neprázdnych) | 35 (35) | 28 (28) |
| Počet slov (bez čísel slôh) | 118 | 118 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 118 | 118 |
| Riadky s číslom slohy na začiatku (`1.`) | 7 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 7 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 6 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 118 slov v A, 118 slov v B; 1 miest s rozdielom obsahu
1. [preklep / zmena slova] A v6 r.4: `Galileje,`  vs  B v6 r.3: `Galiley,`  [JKS1/2/3 obsahujú podobu A: JKS1✓ JKS2✗ JKS3✗; podobu B: JKS1✗ JKS2✓ JKS3✓]
     - riadok v A: `Náhlite do Galileje,`
     - riadok v B: `Náhlite do Galiley,`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 3
     - interpunkcia: A v4 r.4 `»Hrob` vs B v4 r.3 `Hrob`; A v4 r.5 `mieste«.` vs B v4 r.4 `mieste.`; A v6 r.5 `uzriete.«` vs B v6 r.4 `uzriete.`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `Galileje,`×1; viac v B: `Galiley,`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `detsky zbor` · tituly: `209. Obeť svoju veľkonočnú` · text (slová, ktoré v žiadnom inom súbore nie sú): v6 r.4: `Galileje,`
- **B**: tagy: – · tituly: `209. Obeť svoju veľkonočnú (bez čísel)` · text (slová, ktoré v žiadnom inom súbore nie sú): v6 r.3: `Galiley,`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3, len referencia)**

| Referencia | A | B |
|---|---|---|
| `209. Obeť svoju veľkonočnú (JKS1).xml` (118 slov, slohy: v1 v2 v3 v4 v5 v6 v7) | 118 slov, rozdiel 1 (zhoda 99 %) | 118 slov, rozdiel 2 (zhoda 98 %) |
| `209. Obeť svoju veľkonočnú (JKS2).xml` (123 slov, slohy: v1 v2 v3 v4 v5 v6 v7) | 118 slov, rozdiel 6 (zhoda 95 %) | 118 slov, rozdiel 5 (zhoda 96 %) |
| `209. Obeť svoju veľkonočnú (JKS3).xml` (118 slov, slohy: v1 v2 v3 v4 v5 v6 v7) | 118 slov, rozdiel 1 (zhoda 99 %) | 118 slov, rozdiel 0 (zhoda 100 %) |

**Odporúčanie**

- **Ponechať:** obe – `209. Obeť svoju veľkonočnú (JKS, Veľkonočná, detsky zbor).xml` + `209. Obeť svoju veľkonočnú (bez čísel) (JKS, Veľkonočná).xml` (A a B)
- **Zmazať / zlúčiť:** nič.
- **Prečo:**
  - B má v titule `209. Obeť svoju veľkonočnú (bez čísel)` – ide o pomenovanú variantu bez čísel slôh (4 riadky na slohu), A má v každej sloha navyše samostatný riadok s číslom slohy a značkou piesne (`1.` … `209`, spolu 5 riadkov na slohu).
  - Obsahovo sa líšia len `Galileje,` (A, v6 r.4) vs `Galiley,` (B, v6 r.3) a interpunkcia: A má »Hrob … mieste«. a …uzriete.«, B ich nemá.
  - Tvar `Galiley` poznajú referencie JKS2 a JKS3 (B je s JKS3 slovo po slove totožná), tvar `Galileje` len JKS1 – poznámka v duplicity.md, že `Galiley` je preklep, sa teda skriptom nepotvrdila.
  - A už obsahuje zlúčený tag `detsky zbor`; B nemá žiadny unikátny text ani tag, len variantu rozloženia.
- **Čo prevziať z ostatných:**
  - Ak sa súbory zlúčia: do jedného dať jednotnú podobu `Galiley`/`Galileje` (treba rozhodnúť podľa tlačeného JKS) a rozhodnúť, či ponechať »…« úvodzovky.
- **Istota:** stredná – Obsah je rovnaký, ale nedá sa overiť, či je „bez čísel“ variant stále potrebná.

**Riziká a neistoty:**

- Správny tvar `Galiley`/`Galileje` je neisté – treba skontrolovať tlačený spevník.
- Ak sa B zmaže, stratí sa rozloženie bez riadku s číslom slohy.

---

<a id="g3"></a>
## G3 · [4a] `217. (Duch svätý, JKS).xml` · `Duchu Svätý, príď z neba (detsky zbor).xml`

**Zhrnutie:** A má všetkých 7 slôh s vypísaným refrénom (169 slov), B má refrén len ako `atď.`, `verseOrder` hrá iba 3 slohy a časť textu je omylom v `<chord>`.

**Súbory v skupine:**
- **A** = `217. (Duch svätý, JKS).xml`
- **B** = `Duchu Svätý, príď z neba (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `217.` | `Duchu Svätý, príď z neba` |
| Tagy (`<author>`) | `JKS`, `Duch svätý` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | `v1 v2 v3 c1` |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4 v5 v6 v7` | `v1 v2 v3 v4 v5 v6 v7 c1` |
| Počet slôh / `<lines>` blokov | 7 / 7 | 8 / 15 |
| Počet riadkov (neprázdnych) | 35 (35) | 15 (15) |
| Počet slov (bez čísel slôh) | 169 | 115 |
| verseOrder vs dokument | – | líši sa od poradia v dokumente; nepoužité: v6, v4, v5, v7 |
| Slov po rozbalení verseOrder | 169 | 54 |
| Riadky s číslom slohy na začiatku (`1.`) | 7 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 7 |
| Text omylom v `<chord>` (chyba formátu) | – | `žiaru svetla pravého.:` |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 7 | 0 |
| Riadky s dvojitou medzerou vnútri | 1 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 14 | 12 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 7 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- B v2 r.2: `[: svetlo srdca bôlneho.:] Príď k nám atď.`
- B v3 r.3: `[:ty sladké občerstvenie.:] Príď k nám atď.`
- B v4 r.2: `[:v plači si potešenie.:] Príď k nám atď.`
- B v5 r.2: `[:ľudu tebe verného.:] Príď k nám atď.`
- B v6 r.2: `[:nie je v ňom nič dobrého.:] Príď k nám atď.`
- B v7 r.2: `[:uzdrav, čo je ranené.:] Príď k nám atď.`
- B c1 r.1: `R:Príď k nám, príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 169 slov v A, 115 slov v B; 7 miest s rozdielom obsahu
1. [chýba v B] A v1 r.4 – v2 r.1: `príď k nám, Duchu Svätý, príď k nám Duchu presvätý. Príď k nám,` – v B tento text nie je
2. [iný text] A v2 r.4–5: `príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`  vs  B v2 r.2: `atď.`
3. [iný text] A v3 r.4–5: `príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`  vs  B v3 r.3: `atď.`
4. [iný text] A v4 r.4–5: `príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`  vs  B v4 r.2: `atď.`
5. [iný text] A v5 r.4–5: `príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`  vs  B v5 r.2: `atď.`
6. [iný text] A v6 r.4–5: `príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`  vs  B v6 r.2: `atď.`
7. [chýba v A] B v7 r.2 – c1 r.1: `atď. R:Príď k nám,` – v A tento text nie je  [JKS1/2/3: JKS1✗ JKS2✗ JKS3✗]
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 7, značky opakovania: 11
     - interpunkcia: A v1 r.3 `pravého.` vs B v1 r.1 `pravého.:`; A v2 r.4 `nám,` vs B v2 r.2 `nám`; A v3 r.4 `nám,` vs B v3 r.3 `nám`; A v4 r.4 `nám,` vs B v4 r.2 `nám`; A v5 r.4 `nám,` vs B v5 r.2 `nám`; A v6 r.4 `nám,` vs B v6 r.2 `nám`; A v7 r.4 `nám,` vs B v7 r.2 `nám`
     - značky opakovania: A v2 r.3 `bôlneho.` vs B v2 r.2 `bôlneho.:]`; A v3 r.3 `ty` vs B v3 r.3 `[:ty`; A v3 r.3 `občerstvenie.` vs B v3 r.3 `občerstvenie.:]`; A v4 r.3 `v` vs B v4 r.2 `[:v`; A v4 r.3 `potešenie.` vs B v4 r.2 `potešenie.:]`; A v5 r.3 `ľudu` vs B v5 r.2 `[:ľudu`; A v5 r.3 `verného.` vs B v5 r.2 `verného.:]`; A v6 r.3 `nie` vs B v6 r.2 `[:nie` … (+3)
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `Duchu`×12, `k`×12, `nám,`×12, `presvätý.`×6, `príď`×13, `Svätý,`×6; viac v B: `atď.`×6, `R:Príď`×1
   - V poradí hrania (po rozbalení verseOrder): 169 vs 54 slov, 3 miest s rozdielom obsahu: A `príď k nám, Duchu Svätý, príď k nám … (13 slov)` vs B ``; A `` vs B `k nám atď. Najvernejší tešiteľ, poslal ta nám … (17 slov)`; A `Najvernejší tešiteľ, poslal ta nám Spasiteľ; ty sladké … (119 slov)` vs B ``

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Duch svätý`, `JKS` · tituly: `217.` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.4 – v2 r.1: `príď k nám, Duchu Svätý, príď k nám Duchu presvätý. Príď k nám,`; v2 r.4–5: `príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`; v3 r.4–5: `príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`; v4 r.4–5: `príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`; v5 r.4–5: `príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`; v6 r.4–5: `príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`
- **B**: tagy: `detsky zbor` · tituly: `Duchu Svätý, príď z neba` · verseOrder `v1 v2 v3 c1` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.2: `atď.`; v3 r.3: `atď.`; v4 r.2: `atď.`; v5 r.2: `atď.`; v6 r.2: `atď.`; v7 r.2 – c1 r.1: `atď. R:Príď k nám,`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3, len referencia)**

| Referencia | A | B |
|---|---|---|
| `217. Duchu Svätý, príď z neba (JKS1).xml` (115 slov, slohy: v1 v2 v3 v4 v5 v6 v7) | 169 slov, rozdiel 60 (zhoda 64 %) | 115 slov, rozdiel 13 (zhoda 89 %) |
| `217. Duchu Svätý, príď z neba (JKS2).xml` (164 slov, slohy: v1 v2 v3 v4 v5 v6 v7 v8 v9 v10) | 169 slov, rozdiel 70 (zhoda 59 %) | 115 slov, rozdiel 72 (zhoda 56 %) |
| `217. Duchu Svätý, príď z neba (JKS3).xml` (169 slov, slohy: v1 v2 v3 v4 v5 v6 v7) | 169 slov, rozdiel 1 (zhoda 99 %) | 115 slov, rozdiel 64 (zhoda 62 %) |

**Odporúčanie**

- **Ponechať:** `217. (Duch svätý, JKS).xml` (A)
- **Zmazať / zlúčiť:** `Duchu Svätý, príď z neba (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B má `verseOrder` `v1 v2 v3 c1`, takže slohy v4–v7 sa nikdy nezobrazia; po rozbalení má B len 54 slov oproti 169 v A.
  - V B je text `žiaru svetla pravého.:` uložený omylom ako názov akordu (`<chord name="…"/>`), takže sa na slajde nezobrazí (chyba formátu, nie verzia s akordmi).
  - B skracuje refrén na `Príď k nám atď.` (v2 r.2, v3 r.3, v4 r.2, v5 r.2, v6 r.2, v7 r.2) a čísla slôh sú zlepené so slovom (`1Duchu`, `2Príď`, … 7 riadkov).
  - A zodpovedá referencii JKS3 (rozdiel 1 slovo), B má rozdiel 64 slov (zhoda 62 %).
  - A však nemá názov piesne: titul je len `217.` (B má `Duchu Svätý, príď z neba`, rovnaký názov majú JKS1/JKS2/JKS3).
- **Čo prevziať z ostatných:**
  - Do A doplniť titul «217. Duchu Svätý, príď z neba» (názov z B a referencií).
  - Pridať tag `detsky zbor`; súbor by sa potom volal «217. Duchu Svätý, príď z neba (Duch svätý, JKS, detsky zbor).xml».
- **Istota:** vysoká – A je úplný nadmnožina B; B je neúplný a má chybu formátu.

**Riziká a neistoty:**

- Skupina 55 (`Pieseň k Duchu Svätému` z Večeradla) sa týka tej istej piesne 217 – pozri tam.
- Presný nový názov súboru je návrh podľa konvencie, nie overené OpenLP exportom.

---

<a id="g4"></a>
## G4 · [4a] `244. K stolu božej láskavosti (JKS, Začiatok).xml` · `244 jks (detsky zbor).xml`

**Zhrnutie:** Rovnaký text; B má každú z 5 slôh na jednom dlhom riadku, A je rozdelená na 9 riadkov a má oddiely `Glória:`, `Krédo:`, `Ofertórium:`, `Sanktus:`.

**Súbory v skupine:**
- **A** = `244. K stolu božej láskavosti (JKS, Začiatok).xml`
- **B** = `244 jks (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `244. K stolu božej láskavosti` | `244 jks` |
| Tagy (`<author>`) | `JKS`, `Začiatok` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4 v5` | `v1 v2 v3 v4 v5` |
| Počet slôh / `<lines>` blokov | 5 / 5 | 5 / 5 |
| Počet riadkov (neprázdnych) | 45 (45) | 5 (5) |
| Počet slov (bez čísel slôh) | 154 | 146 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 154 | 146 |
| Riadky s číslom slohy na začiatku (`1.`) | 1 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 5 | 0 |
| Riadky s dlhým radom medzier (3+) | 5 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 10 | 10 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- A v2 r.1: `Glória: 2.                                  244.`
- A v3 r.1: `Krédo: 3.                                  244.`
- A v4 r.1: `Ofertórium: 4.                         244.`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 154 slov v A, 146 slov v B; 4 miest s rozdielom obsahu
1. [chýba v B] A v2 r.1: `Glória: 2.` – v B tento text nie je  [JKS1/2/3: JKS1✗ JKS2✗ JKS3✗]
2. [chýba v B] A v3 r.1: `Krédo: 3.` – v B tento text nie je  [JKS1/2/3: JKS1✗ JKS2✗ JKS3✗]
3. [chýba v B] A v4 r.1: `Ofertórium: 4.` – v B tento text nie je  [JKS1/2/3: JKS1✗ JKS2✗ JKS3✗]
4. [chýba v B] A v5 r.1: `Sanktus: 5.` – v B tento text nie je  [JKS1/2/3: JKS1✗ JKS2✗ JKS3✗]
   - Rozdiely len v zápise (rovnaké slová): značky opakovania: 10
     - značky opakovania: A v1 r.6 `keď` vs B v1 r.1 `[:keď`; A v1 r.9 `vykonávame.` vs B v1 r.1 `vykonávame.:]`; A v2 r.6 `Ty,` vs B v2 r.1 `[:Ty,`; A v2 r.9 `prisluhujeme.` vs B v2 r.1 `prisluhujeme.:]`; A v3 r.6 `pod` vs B v3 r.1 `[:pod`; A v3 r.9 `zjavnej.` vs B v3 r.1 `zjavnej.:]`; A v4 r.6 `obeť` vs B v4 r.1 `[:obeť`; A v4 r.9 `pristupuje.` vs B v4 r.1 `pristupuje.:]` … (+2)
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `2.`×1, `3.`×1, `4.`×1, `5.`×1, `Glória:`×1, `Krédo:`×1, `Ofertórium:`×1, `Sanktus:`×1; viac v B: –

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `JKS`, `Začiatok` · tituly: `244. K stolu božej láskavosti` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.1: `Glória: 2.`; v3 r.1: `Krédo: 3.`; v4 r.1: `Ofertórium: 4.`; v5 r.1: `Sanktus: 5.`
- **B**: tagy: `detsky zbor` · tituly: `244 jks` · text: nič unikátne

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3, len referencia)**

| Referencia | A | B |
|---|---|---|
| `244. K stolu božej láskavosti (JKS1).xml` (149 slov, slohy: v1 v2 v3 v4 v5) | 154 slov, rozdiel 5 (zhoda 97 %) | 146 slov, rozdiel 4 (zhoda 97 %) |
| `244. K stolu Božej láskavosti (JKS2).xml` (150 slov, slohy: v1 v2 v3 v4 v5) | 154 slov, rozdiel 5 (zhoda 97 %) | 146 slov, rozdiel 5 (zhoda 97 %) |
| `244. K stolu Božej láskavosti (JKS3).xml` (146 slov, slohy: v1 v2 v3 v4 v5) | 154 slov, rozdiel 8 (zhoda 95 %) | 146 slov, rozdiel 0 (zhoda 100 %) |

**Odporúčanie**

- **Ponechať:** `244. K stolu božej láskavosti (JKS, Začiatok).xml` (A)
- **Zmazať / zlúčiť:** `244 jks (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Slovný rozdiel je len v 4 označeniach častí omše, ktoré má iba A: `Glória: 2.` (v2 r.1), `Krédo: 3.` (v3 r.1), `Ofertórium: 4.` (v4 r.1), `Sanktus: 5.` (v5 r.1).
  - B má 5 riadkov (jedna sloha = jeden riadok, 146 slov), A 45 riadkov; na slajde je riadok s priemerne 29 slovami ťažko čitateľný.
  - A má JKS rozloženie (`244.` ako koncová značka pri 5 slohách) a tag `Začiatok`; B nemá žiadny unikátny text.
  - Značky opakovania sú v oboch (10 : 10), líšia sa len rozložením (`[:keď` … `vykonávame.:]` v B je na jednom riadku).
- **Čo prevziať z ostatných:**
  - Pridať tag `detsky zbor`.
- **Istota:** vysoká – B je len spojený zápis toho istého textu bez oddielov.

**Riziká a neistoty:**

- Pri JKS3 je zhoda B 100 %, A 95 % – rozdiel však tvoria práve označenia častí omše, ktoré JKS3 nemá.

---

<a id="g5"></a>
## G5 · [4a] `039. Búvaj, Dieťa krásne (JKS, Vianočná).xml` · `Buvaj dieta krasne A-dur jednoduchy (detsky zbor).xml`

**Zhrnutie:** Rovnaký text; B má delené slabiky (`mi-lý`) a 3 chyby (`Ježiško`, `poteší,na`, `ďiaľky,`), A má jeden preklep v interpunkcii (opačný apostrof namiesto čiarky v riadku «abys` mohol dobre spať.»).

Existuje aj verzia s akordmi: `Buvaj dieta krasne A-dur jednoduchy (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `039. Búvaj, Dieťa krásne (JKS, Vianočná).xml`
- **B** = `Buvaj dieta krasne A-dur jednoduchy (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `039. Búvaj, Dieťa krásne` | `Buvaj dieta krasne A-dur jednoduchy` |
| Tagy (`<author>`) | `Vianočná`, `JKS` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3` | `v1 v2 v3` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 3 / 3 |
| Počet riadkov (neprázdnych) | 27 (27) | 15 (15) |
| Počet slov (bez čísel slôh) | 93 | 92 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 93 | 92 |
| Riadky s číslom slohy na začiatku (`1.`) | 3 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 3 | 0 |
| Riadky s dlhým radom medzier (3+) | 3 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | CRLF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 93 slov v A, 92 slov v B; 2 miest s rozdielom obsahu
1. [preklep / zmena slova] A v1 r.8: `Ježišku`  vs  B v1 r.4: `Ježiško`  [JKS1/2/3 obsahujú podobu A: JKS1✓ JKS2✓ JKS3✓; podobu B: JKS1✗ JKS2✗ JKS3✗]
     - riadok v A: `Ježišku náš milý, aby sa ti snili`
     - riadok v B: `Ježiško náš mi-lý, aby sa ti snili`
2. [preklep / zmena slova] A v2 r.4–5: `poteší na`  vs  B v2 r.2: `poteší,na`  [JKS1/2/3 obsahujú podobu A: JKS1✓ JKS2✓ JKS3✓; podobu B: JKS1✗ JKS2✗ JKS3✗]
     - riadok v A: `nech sa Dieťa poteší`
     - riadok v B: `nech sa Dieťa poteší,na tom našom salaši.`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 12, veľkosť písmen: 2, diakritika: 1
     - interpunkcia: A v1 r.3 `jasle` vs B v1 r.1 `jasle,`; A v1 r.4 `Pachoľa;` vs B v1 r.2 `Pachoľa,`; A v1 r.7 `abys`` vs B v1 r.3 `abys,`; A v1 r.8 `milý,` vs B v1 r.4 `mi-lý,`; A v2 r.7 `muzika;` vs B v2 r.3 `muzika!`; A v2 r.8 `vami` vs B v2 r.4 `va-mi`; A v2 r.8 `jasľami` vs B v2 r.4 `jasľa-mi,`; A v2 r.9 `milému.` vs B v2 r.5 `mi-lé-mu.` … (+4)
     - veľkosť písmen: A v2 r.8 `my` vs B v2 r.4 `My`; A v3 r.3 `dieťa` vs B v3 r.1 `Dieťa`
     - diakritika: A v3 r.7 `diaľky,` vs B v3 r.3 `ďiaľky,`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `Ježišku`×1, `na`×1, `poteší`×1; viac v B: `Ježiško`×1, `poteší,na`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `JKS`, `Vianočná` · tituly: `039. Búvaj, Dieťa krásne` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.8: `Ježišku`; v2 r.4–5: `poteší na`
- **B**: tagy: `detsky zbor` · tituly: `Buvaj dieta krasne A-dur jednoduchy` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.4: `Ježiško`; v2 r.2: `poteší,na`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3, len referencia)**

| Referencia | A | B |
|---|---|---|
| `039. Buvaj, dieťa krásne (JKS1).xml` (93 slov, slohy: v1 v2 v3) | 93 slov, rozdiel 0 (zhoda 100 %) | 92 slov, rozdiel 3 (zhoda 97 %) |
| `039. Búvaj, Dieťa krásne (JKS2).xml` (93 slov, slohy: v1 v2 v3) | 93 slov, rozdiel 2 (zhoda 98 %) | 92 slov, rozdiel 5 (zhoda 95 %) |
| `039. Búvaj, Dieťa krásne (JKS3).xml` (93 slov, slohy: v1 v2 v3) | 93 slov, rozdiel 0 (zhoda 100 %) | 92 slov, rozdiel 3 (zhoda 97 %) |

**Odporúčanie**

- **Ponechať:** `039. Búvaj, Dieťa krásne (JKS, Vianočná).xml` (A)
- **Zmazať / zlúčiť:** `Buvaj dieta krasne A-dur jednoduchy (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A zodpovedá referenciám JKS1 a JKS3 slovo po slove (rozdiel 0), B sa od nich líši v 3 slovách (zhoda 97 %).
  - B: `Ježiško náš mi-lý` (v1 r.4) – zlý vokatív (A: `Ježišku`); `poteší,na` (v2 r.2) zlepené; `ďiaľky,` (v3 r.3) chybná diakritika (A: `diaľky,`).
  - B delí slabiky (`mi-lý`, `va-mi`, `jasľa-mi,`, `mi-lé-mu.`) – na slajde by sa zobrazili pomlčky; A má normálny text.
  - B nemá žiadny unikátny text ani tag okrem `detsky zbor`; B má ako jediný v skupine konce riadkov CRLF.
- **Čo prevziať z ostatných:**
  - V A (v1 r.7) opraviť «abys` mohol dobre spať.» na «abys, mohol dobre spať.».
  - Pridať tag `detsky zbor`.
- **Istota:** vysoká – A je bez chýb obsahu a zodpovedá referenciám; B má viac preklepov.

**Riziká a neistoty:**

- Delenie slabík v B môže slúžiť na spev detí; ak je to zámer, treba to riešiť inak (nie samostatným súborom).

---

<a id="g6"></a>
## G6 · [4a] `295. Vitaj, milý Jezu Kriste (Eucharistické, JKS).xml` · `JKS Vitaj milý Jezu (detsky zbor).xml`

**Zhrnutie:** B (jeden riadok na slohu) nemá 6. slohu; zvyšok je rovnaký.

**Súbory v skupine:**
- **A** = `295. Vitaj, milý Jezu Kriste (Eucharistické, JKS).xml`
- **B** = `JKS Vitaj milý Jezu (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `295. Vitaj, milý Jezu Kriste` | `JKS Vitaj milý Jezu` |
| Tagy (`<author>`) | `Eucharistické`, `JKS` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4 v5 v6` | `v1 v2 v3 v4 v5` |
| Počet slôh / `<lines>` blokov | 6 / 6 | 5 / 5 |
| Počet riadkov (neprázdnych) | 30 (30) | 5 (5) |
| Počet slov (bez čísel slôh) | 105 | 89 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 105 | 89 |
| Riadky s číslom slohy na začiatku (`1.`) | 1 | 5 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 1 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 105 slov v A, 89 slov v B; 2 miest s rozdielom obsahu
1. [preklep / zmena slova] A v1 r.4–5: `Telo, čo`  vs  B v1 r.1: `Telo,čo`  [JKS1/2/3 obsahujú podobu A: JKS1✓ JKS2✓ JKS3✓; podobu B: JKS1✗ JKS2✗ JKS3✗]
     - riadok v A: `vitaj, drahé Božie Telo,`
     - riadok v B: `1. Vitaj, milý Jezu Kriste, vitaj Synu Panny čistej, vitaj, drahé Božie Telo,čo za nás na kríži pnelo!`
2. [chýba v B] A v6 r.2–5: `Bože, prv ako umrieme, túto Sviatosť nech prijmeme všetkých hriechov odpustenie, duše našej na … (15 slov)` – v B tento text nie je
   - Žiadne rozdiely v zápise (diakritika / veľkosť / interpunkcia) pri zhodných slovách.
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `ako`×1, `Bože,`×1, `čo`×1, `duše`×1, `hriechov`×1, `na`×1, `našej`×1, `nech`×1, `odpustenie,`×1, `prijmeme`×1, `prv`×1, `spasenie.`×1, `Sviatosť,`×1, `Telo,`×1, `túto`×1, `umrieme,`×1, `všetkých`×1; viac v B: `Telo,čo`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Eucharistické`, `JKS` · tituly: `295. Vitaj, milý Jezu Kriste` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.4–5: `Telo, čo`; v6 r.2–5: `Bože, prv ako umrieme, túto Sviatosť nech prijmeme všetkých hriechov odpustenie, duše našej na spasenie.`
- **B**: tagy: `detsky zbor` · tituly: `JKS Vitaj milý Jezu` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1: `Telo,čo`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3, len referencia)**

| Referencia | A | B |
|---|---|---|
| `295. Vitaj milý Jezu Kriste (JKS1).xml` (105 slov, slohy: v1 v2 v3 v4 v5 v6) | 105 slov, rozdiel 0 (zhoda 100 %) | 89 slov, rozdiel 17 (zhoda 84 %) |
| `295. Vitaj milý Jezu Kriste (JKS2).xml` (105 slov, slohy: v1 v2 v3 v4 v5 v6) | 105 slov, rozdiel 0 (zhoda 100 %) | 89 slov, rozdiel 17 (zhoda 84 %) |
| `295. Vitaj milý Jezu Kriste (JKS3).xml` (105 slov, slohy: v1 v2 v3 v4 v5 v6) | 105 slov, rozdiel 0 (zhoda 100 %) | 89 slov, rozdiel 17 (zhoda 84 %) |

**Odporúčanie**

- **Ponechať:** `295. Vitaj, milý Jezu Kriste (Eucharistické, JKS).xml` (A)
- **Zmazať / zlúčiť:** `JKS Vitaj milý Jezu (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B nemá celú 6. slohu: `Bože, prv ako umrieme, túto Sviatosť nech prijmeme všetkých hriechov odpustenie, duše našej na spasenie.` (A, v6 r.2–5); B má 5 slôh a 89 slov oproti 105.
  - A sa zhoduje so všetkými referenciami JKS1, JKS2 aj JKS3 na 100 %; B má rozdiel 17 slov (zhoda 84 %).
  - B má `Telo,čo` (v1 r.1) – zlepené bez medzery; každá sloha je jeden riadok s číslom `1.`.
- **Čo prevziať z ostatných:**
  - Pridať tag `detsky zbor`.
- **Istota:** vysoká – B je podmnožina A.

**Riziká a neistoty:**

- Ak detský zbor spieva len 5 slôh, musí sa to riešiť cez `verseOrder` v A, nie samostatným súborom.

---

<a id="g7"></a>
## G7 · [4a] `484. Yzopom ma pokrop Pane (JKS).xml` · `Yzopom (detsky zbor).xml`

**Zhrnutie:** B obsahuje iba prvé dve slohy (variant 484a „Yzopom“), A má všetky štyri (aj „Tiekla voda“, variant 484b).

**Súbory v skupine:**
- **A** = `484. Yzopom ma pokrop Pane (JKS).xml`
- **B** = `Yzopom (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `484. Yzopom ma pokrop Pane` | `Yzopom` |
| Tagy (`<author>`) | `JKS` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4` | `v1 v2` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 2 / 2 |
| Počet riadkov (neprázdnych) | 4 (4) | 8 (8) |
| Počet slov (bez čísel slôh) | 124 | 63 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 124 | 63 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 4 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 124 slov v A, 63 slov v B; 1 miest s rozdielom obsahu
1. [chýba v B] A v3 r.1 – v4 r.1: `Tiekla voda z pravej strany svätyne, aleluja, krstom v nej sme povolaní k nevine, … (61 slov)` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 6
     - interpunkcia: A v1 r.1 `dušu,` vs B v1 r.2 `dušu`; A v1 r.1 `//Zmiluj` vs B v1 r.3 `Zmiluj`; A v1 r.1 `nečnosti.//` vs B v1 r.4 `nečnosti.:/`; A v2 r.1 `Synu,` vs B v2 r.1 `Synu`; A v2 r.1 `//Zmiluj` vs B v2 r.3 `Zmiluj`; A v2 r.1 `nečnosti.//` vs B v2 r.4 `nečnosti.:/`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `aleluja,`×2, `Bohu`×1, `Bože,`×2, `dobrotivý,`×1, `i`×1, `je`×2, `k`×2, `krstom`×1, `milosti,`×2, `milostivý`×1, `môže`×2, `na`×1, `nad`×2, `nám`×1, `nami,`×2, `naše`×2, `nečnosti.//`×2, `nej`×1, `nekonečnej`×2, `nevine,`×1, `On`×1, `povolaní`×1, `pravej`×1, `sa`×2, `sme`×1, `srdečné!`×1, `strany`×1, `svätyne,`×1, `Tiekla`×1, `tvoje`×2, `v`×3, `včuľ`×1, `vďaky`×1, `večné.`×1, `veky`×1, `voda`×1, `vzdajme`×1, `vždy`×1, `z`×1, `že`×1, `zľutovanie`×2, `//Zmiluj`×2, `zotrieť`×2; viac v B: –

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `JKS` · tituly: `484. Yzopom ma pokrop Pane` · text (slová, ktoré v žiadnom inom súbore nie sú): v3 r.1 – v4 r.1: `Tiekla voda z pravej strany svätyne, aleluja, krstom v nej sme povolaní k nevine, aleluja! //Zmiluj … (61 slov)`
- **B**: tagy: `detsky zbor` · tituly: `Yzopom` · text: nič unikátne

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3, len referencia)**

| Referencia | A | B |
|---|---|---|
| `484a. Yzopom ma pokrop, Pane (JKS2).xml` (63 slov, slohy: v1 v2) | 124 slov, rozdiel 61 (zhoda 51 %) | 63 slov, rozdiel 0 (zhoda 100 %) |
| `484b. Tiekla voda z pravej strany (JKS2).xml` (61 slov, slohy: v1 v2) | 124 slov, rozdiel 63 (zhoda 49 %) | 63 slov, rozdiel 33 (zhoda 48 %) |
| `484. Tiekla voda z pravej strany (JKS3).xml` (124 slov, slohy: v1 v2 v3 v4) | 124 slov, rozdiel 0 (zhoda 100 %) | 63 slov, rozdiel 61 (zhoda 51 %) |

**Odporúčanie**

- **Ponechať:** `484. Yzopom ma pokrop Pane (JKS).xml` (A)
- **Zmazať / zlúčiť:** `Yzopom (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Slovo po slove sa B zhoduje s A v slohách v1–v2; A má navyše v3–v4 (`Tiekla voda z pravej strany svätyne, aleluja, …`, 61 slov).
  - B sa zhoduje s referenciou JKS2 484a na 100 %; A sa zhoduje s JKS3 484 na 100 % (JKS3 má 4 slohy ako A).
  - B nemá unikátny text ani tag okrem `detsky zbor`; zápis opakovania je v B `/: Zmiluj sa nad nami, Bože, v nekonečnej milosti,` … `naše nečnosti.:/`, v A `//Zmiluj` … `nečnosti.//`.
- **Čo prevziať z ostatných:**
  - Pridať tag `detsky zbor`; ak detský zbor spieva len prvé dve slohy, v A pridať `verseOrder` `v1 v2`.
- **Istota:** vysoká – B je podmnožina A (slovo po slove).

**Riziká a neistoty:**

- Zmazaním B sa stratí „krátka“ verzia ako samostatná pieseň; spieva sa ale ako výber slôh.

---

<a id="g8"></a>
## G8 · [4a] `365 (JKS).xml` · `365 Pod tvoj plášť sa utiekame, (JKS).xml`

**Zhrnutie:** B má len prvé 4 zo 7 slôh; A je úplná (213 slov) a zhoduje sa s JKS1 na 100 %. Obe majú v texte oddeľovače ` - ` a treba ich preformátovať.

**Súbory v skupine:**
- **A** = `365 (JKS).xml`
- **B** = `365 Pod tvoj plášť sa utiekame, (JKS).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `365`<br>`Pod Tvoj plášť sa utiekame` | `365 Pod tvoj plášť sa utiekame,` |
| Tagy (`<author>`) | `JKS` | `JKS` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1a v1b v1c v1d v1e v1f v1g` | `v1 v2 v3 v4` |
| Počet slôh / `<lines>` blokov | 7 / 7 | 4 / 4 |
| Počet riadkov (neprázdnych) | 13 (7) | 16 (16) |
| Počet slov (bez čísel slôh) | 213 | 122 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 213 | 122 |
| Riadky s číslom slohy na začiatku (`1.`) | 7 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 6 | 0 |
| Riadky s koncovou medzerou | 0 | 2 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 213 slov v A, 122 slov v B; 1 miest s rozdielom obsahu
1. [chýba v B] A v1e r.1 – v1g r.1: `Keď opustíš nás v žalosti, Potešenie premilé, kto poteší nás v úzkosti pri poslednej … (91 slov)` – v B tento text nie je
   - Žiadne rozdiely v zápise (diakritika / veľkosť / interpunkcia) pri zhodných slovách.
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `dúfa.`×1, `hlasu`×1, `hodine.`×1, `hroznú`×1, `jeho`×1, `Ježiša,`×1, `Keď`×1, `Krista`×1, `kto`×1, `Mária,`×3, `Matka`×3, `nás,`×10, `naša`×3, `Nedaj,`×6, `ó`×3, `Ochráň,`×3, `od`×1, `on`×1, `opustíš`×1, `osloboď`×1, `Pána,`×1, `päť`×1, `poslednej`×1, `Potešenie`×1, `poteší`×1, `požehnaná,`×1, `premilá!`×3, `premilé,`×1, `preto`×1, `pri`×1, `pros`×1, `prosíme`×1, `rán`×1, `si`×1, `Skrze`×2, `smrť`×1, `spanilá!`×3, `svojho,`×1, `Syna`×1, `ťa`×1, `teba`×1, `tvojho,`×1, `U`×1, `úzkosti,`×1, `v`×3, `všíma`×1, `vysloboď`×3, `vždy`×1, `za`×1, `žalosti.`×1, `zastaň,`×3, `zatratiť`×3, `žiadame,`×1, `zlého.`×1; viac v B: –

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: – · tituly: `365`, `Pod Tvoj plášť sa utiekame` · text (slová, ktoré v žiadnom inom súbore nie sú): v1e r.1 – v1g r.1: `Keď opustíš nás v žalosti, Potešenie premilé, kto poteší nás v úzkosti pri poslednej hodine. Ochráň, … (91 slov)`
- **B**: tagy: – · tituly: `365 Pod tvoj plášť sa utiekame,` · text: nič unikátne

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3, len referencia)**

| Referencia | A | B |
|---|---|---|
| `365. Pod tvoj plášť sa utiekame (JKS1).xml` (213 slov, slohy: v1 v2 v3 v4 v5 v6 v7) | 213 slov, rozdiel 0 (zhoda 100 %) | 122 slov, rozdiel 91 (zhoda 57 %) |
| `365. Pod tvoj plášť sa utiekame (JKS2).xml` (141 slov, slohy: v1 v2 v3 v4 v5 v6 v7) | 213 slov, rozdiel 79 (zhoda 63 %) | 122 slov, rozdiel 56 (zhoda 60 %) |

**Odporúčanie**

- **Ponechať:** `365 (JKS).xml` (A)
- **Zmazať / zlúčiť:** `365 Pod tvoj plášť sa utiekame, (JKS).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A má 213 slov (7 slôh), B 122; chýba jej text od `5. Keď opustíš nás v žalosti, - Potešenie premilé,` (A, v1e r.1 – v1g r.1, 91 slov).
  - A sa zhoduje s referenciou JKS1 365 na 100 %, B má rozdiel 91 slov.
  - B nemá žiadny unikátny text; jej titul `365 Pod tvoj plášť sa utiekame,` má navyše čiarku a malé „tvoj“.
  - A má druhý titul `Pod Tvoj plášť sa utiekame`, takže sa názov nestratí.
  - Formát: A má každú sloha na jednom dlhom riadku (cca 30 slov) s oddeľovačmi ` - ` a prázdnym riadkom navyše; B ich delí na 4 riadky (napr. `Pod tvoj plášť sa utiekame, - ó Panenka Mária,`), no `- ` na začiatku riadkov a v strede zostáva aj v B.
- **Čo prevziať z ostatných:**
  - Pri preformátovaní A použiť delenie na 4 riadky ako v B pre slohy 1–4 a rovnaké delenie pre slohy 5–7; oddeľovače ` - ` odstrániť (v obidvoch súboroch sú).
- **Istota:** vysoká – B je presná podmnožina A.

**Riziká a neistoty:**

- Pomenovanie slôh v A (`v1a` … `v1g`) je neštandardné; netýka sa rozhodnutia o zmazaní.
- Číslovanie `1.` … `7.` je v A priamo na začiatku textového riadka (bez rozloženia s dlhým radom medzier).

---

<a id="g9"></a>
## G9 · [4a] `419. K tebe prichádzame (JKS).xml` · `JKS 419 - K tebe prichádzame (JKS).xml`

**Zhrnutie:** B má navyše 3. slohu `Vypros nám u Boha, …`; A má lepšie rozloženie (JKS formát, 12 riadkov).

**Súbory v skupine:**
- **A** = `419. K tebe prichádzame (JKS).xml`
- **B** = `JKS 419 - K tebe prichádzame (JKS).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `419. K tebe prichádzame` | `JKS 419 - K tebe prichádzame` |
| Tagy (`<author>`) | `JKS` | `JKS` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2` | `v1 v2 v3` |
| Počet slôh / `<lines>` blokov | 2 / 2 | 3 / 3 |
| Počet riadkov (neprázdnych) | 12 (12) | 20 (20) |
| Počet slov (bez čísel slôh) | 56 | 80 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 56 | 80 |
| Riadky s číslom slohy na začiatku (`1.`) | 2 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 2 | 0 |
| Riadky s dlhým radom medzier (3+) | 2 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 1 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 56 slov v A, 80 slov v B; 1 miest s rozdielom obsahu
1. [chýba v A] B v3 r.1–5: `Vypros nám u Boha, šťastné skonanie, u svojej nevesty orodovanie; Ježiš, Mária, najsladšie mená, … (24 slov)` – v A tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 8
     - interpunkcia: A v1 r.2 `prichádzame,` vs B v1 r.1 `prichádzame`; A v1 r.3 `nebeskej,` vs B v1 r.3 `nebeskej`; A v1 r.4 `ty,` vs B v1 r.5 `ty`; A v1 r.4 `Kristov,` vs B v1 r.5 `Kristov`; A v1 r.4 `istou,` vs B v1 r.6 `istou;`; A v1 r.5 `vypočuj,` vs B v1 r.7 `vypočuj`; A v1 r.5 `prosíme,` vs B v1 r.7 `prosíme`; A v2 r.3 `nevinnosti,` vs B v2 r.2 `nevinnosti;`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v B: `Boha,`×1, `dychu.`×1, `Ježiš,`×1, `láskavo`×1, `Mária,`×1, `mená,`×1, `na`×1, `najsladšie`×1, `nám`×2, `nášho`×1, `nech`×1, `nevesty`×1, `orodovanie;`×1, `posledným`×1, `šepotom`×1, `skonanie,`×1, `šťastné`×1, `sú`×1, `svojej`×1, `u`×2, `útechu,`×1, `Vypros`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: – · tituly: `419. K tebe prichádzame` · text: nič unikátne
- **B**: tagy: – · tituly: `JKS 419 - K tebe prichádzame` · text (slová, ktoré v žiadnom inom súbore nie sú): v3 r.1–5: `Vypros nám u Boha, šťastné skonanie, u svojej nevesty orodovanie; Ježiš, Mária, najsladšie mená, nech sú … (24 slov)`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3, len referencia)**

| Referencia | A | B |
|---|---|---|
| `419. K tebe prichádzame (JKS1).xml` (80 slov, slohy: v1 v2 v3) | 56 slov, rozdiel 25 (zhoda 69 %) | 80 slov, rozdiel 2 (zhoda 98 %) |
| `419. K tebe prichádzame (JKS2).xml` (80 slov, slohy: v1 v2 v3) | 56 slov, rozdiel 24 (zhoda 70 %) | 80 slov, rozdiel 0 (zhoda 100 %) |

**Odporúčanie**

- **Ponechať:** `419. K tebe prichádzame (JKS).xml` (A)
- **Zmazať / zlúčiť:** `JKS 419 - K tebe prichádzame (JKS).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B má 3 slohy (80 slov), A len 2 (56 slov); 3. sloha (`Vypros nám u Boha, šťastné skonanie, u svojej nevesty orodovanie; Ježiš, Mária, najsladšie mená, … `, 24 slov) je unikátny obsah B.
  - B sa zhoduje s JKS2 na 100 % a s JKS1 na 98 %, A len na ~70 %, lebo tretia sloha chýba; text slôh 1–2 je v A aj B rovnaký (len interpunkcia).
  - B má titul `JKS 419 - K tebe prichádzame` a v1 s 10 riadkami (každý polvers na samostatnom riadku), A má JKS rozloženie s číslom slohy a koncovou značkou `419.`.
- **Čo prevziať z ostatných:**
  - Do A doplniť 3. slohu z B (v3, 5 riadkov) s číslom slohy a koncovou značkou `419.` ako pri slohách 1–2.
- **Istota:** vysoká – Rozdiel je jediná chýbajúca sloha, overená aj voči JKS2.

**Riziká a neistoty:**

- Interpunkcia 3. slohy v B (`nevesty` s malým n) sa líši od JKS2 (`Nevesty`); pri prenose sa dá zjednotiť.

---

<a id="g10"></a>
## G10 · [4a] `536. Ctime túto sviatosť slávnu (JKS).xml` · `JKS 536 - Ctíme túto sviatosť slávnu (JKS).xml`

**Zhrnutie:** Takmer rovnaký text; líši sa `taktiež` (A) vs `tak aj` (B), veľké „S“ a zápis opakovania; A má titul podľa konvencie a slohy rozdelené na slajdy.

**Súbory v skupine:**
- **A** = `536. Ctime túto sviatosť slávnu (JKS).xml`
- **B** = `JKS 536 - Ctíme túto sviatosť slávnu (JKS).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `536. Ctime túto sviatosť slávnu` | `JKS 536 - Ctíme túto sviatosť slávnu` |
| Tagy (`<author>`) | `JKS` | `JKS` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1a v1b v2a v2b` | `v1 v2` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 2 / 2 |
| Počet riadkov (neprázdnych) | 14 (14) | 12 (12) |
| Počet slov (bez čísel slôh) | 42 | 43 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 42 | 43 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 1 | 2 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 4 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 42 slov v A, 43 slov v B; 1 miest s rozdielom obsahu
1. [iný text] A v2a r.4: `taktiež`  vs  B v2 r.4: `tak aj`  [JKS1/2/3 obsahujú podobu A: JKS1✗ JKS3✗ JKS2✓; podobu B: JKS1✓ JKS3✓ JKS2✗]
     - riadok v A: `taktiež dobrorečenie;`
     - riadok v B: `tak aj dobrorečenie;`
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 1, značky opakovania: 4
     - veľkosť písmen: A v1a r.1 `sviatosť` vs B v1 r.1 `Sviatosť`
     - značky opakovania: A v1b r.3 `viera` vs B v1 r.6 `[:viera`; A v1b r.3 `spojená.` vs B v1 r.6 `spojená.:]`; A v2b r.2 `rovnaké` vs B v2 r.6 `[:rovnaké`; A v2b r.2 `uctenie.` vs B v2 r.6 `uctenie.:]`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `taktiež`×1; viac v B: `aj`×1, `tak`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: – · tituly: `536. Ctime túto sviatosť slávnu` · text (slová, ktoré v žiadnom inom súbore nie sú): v2a r.4: `taktiež`
- **B**: tagy: – · tituly: `JKS 536 - Ctíme túto sviatosť slávnu` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.4: `tak aj`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3, len referencia)**

| Referencia | A | B |
|---|---|---|
| `317. Ctime túto sviatosť slávnu (JKS1).xml` (143 slov, slohy: v1 v2 v3 v4 v5 v6 v7 v8 v9 v10) | 42 slov, rozdiel 102 (zhoda 29 %) | 43 slov, rozdiel 100 (zhoda 30 %) |
| `317. Ctime túto Sviatosť slávnu (Sviatosť tela tajomného) (JKS2).xml` (87 slov, slohy: v1 v2 v3) | 42 slov, rozdiel 45 (zhoda 48 %) | 43 slov, rozdiel 46 (zhoda 47 %) |
| `317. Ctime túto Sviatosť slávnu (JKS3).xml` (43 slov, slohy: v1 v2) | 42 slov, rozdiel 2 (zhoda 95 %) | 43 slov, rozdiel 0 (zhoda 100 %) |

**Odporúčanie**

- **Ponechať:** `536. Ctime túto sviatosť slávnu (JKS).xml` (A)
- **Zmazať / zlúčiť:** `JKS 536 - Ctíme túto sviatosť slávnu (JKS).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Jediný obsahový rozdiel: `taktiež dobrorečenie;` (A, v2a r.4) vs `tak aj dobrorečenie;` (B, v2 r.4). V referenciách č. 317 má `taktiež` iba JKS2 (sken tlačeného spevníka), `tak aj` majú JKS1 aj JKS3 (B je s JKS3 slovo po slove totožná).
  - A má titul `536. Ctime túto sviatosť slávnu` podľa konvencie, B má `JKS 536 - Ctíme túto sviatosť slávnu` (s „Ctíme“ v názve, ale „Ctime“ v texte).
  - A je rozdelená na 4 časti (`v1a`, `v1b`, `v2a`, `v2b`) po 3–4 riadkoch, B má 2 slohy po 6 riadkov.
  - B má opakovanie `[:viera s láskou spojená.:]` a `[:rovnaké buď uctenie.:] - Amen.` (Amen v jednom riadku s textom), A má `Amen.` na vlastnom riadku bez značiek opakovania.
- **Čo prevziať z ostatných:**
  - Rozhodnúť o `taktiež`/`tak aj` (väčšina referencií má `tak aj`, tlačený sken `taktiež`) a prípadne do A prevziať značky opakovania `[: :]` (sú aj v JKS3).
- **Istota:** stredná – Odporúčanie A je jasné pre formát, ale výber slova nevieme overiť podľa tlačeného spevníka.

**Riziká a neistoty:**

- Referencie JKS1/2/3 sú v tejto skupine brané z č. 317, lebo pod č. 536 sa pieseň v importoch nenachádza (text je ten istý, číslo 536 označuje len melódiu – pozri duplicity.md, časť 2).

---

<a id="g11"></a>
## G11 · [4c] `Boh je láska (...).xml` · `Boh je láska (Author Unknown).xml`

**Zhrnutie:** B je znehodnotená 64 úvodzovkami (32 na začiatku a 32 na konci druhého riadku) a má iné slovo na konci (`nám` vs `sám`).

**Súbory v skupine:**
- **A** = `Boh je láska (...).xml`
- **B** = `Boh je láska (Author Unknown).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Boh je láska` | `Boh je láska` |
| Tagy (`<author>`) | `...` | `Author Unknown` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `c1` | `v1` |
| Počet slôh / `<lines>` blokov | 1 / 1 | 1 / 1 |
| Počet riadkov (neprázdnych) | 2 (2) | 3 (3) |
| Počet slov (bez čísel slôh) | 17 | 17 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 17 | 17 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 2 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 17 slov v A, 17 slov v B; 1 miest s rozdielom obsahu
1. [preklep / zmena slova] A c1 r.2: `sám.`  vs  B v1 r.3: `nám.`
     - riadok v A: `miluj blížneho tak ako seba, vraví Ježiš sám. :]`
     - riadok v B: `Vraví Ježiš nám.`
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 3, interpunkcia: 2
     - veľkosť písmen: A c1 r.1 `Láska` vs B v1 r.1 `láska`; A c1 r.2 `miluj` vs B v1 r.2 `""""""""""""""""""""""""""""""""Miluj`; A c1 r.2 `vraví` vs B v1 r.3 `Vraví`
     - interpunkcia: A c1 r.1 `dal,` vs B v1 r.1 `dal`; A c1 r.2 `seba,` vs B v1 r.2 `seba!""""""""""""""""""""""""""""""""`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `sám.`×1; viac v B: `nám`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `...` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.2: `sám.`
- **B**: tagy: `Author Unknown` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.3: `nám.`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Boh je láska (...).xml` (A)
- **Zmazať / zlúčiť:** `Boh je láska (Author Unknown).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B má v druhom riadku 64× znak `"` (32 pred slovom `Miluj` a 32 za slovom `seba!`), čo by sa zobrazilo na slajde; A takú chybu nemá.
  - A má refrén uzavretý do `[: … :]` a text na 2 riadkoch (`Boh je Láska a zákon lásky nám On dal,`); B píše `Boh je láska a zákon lásky nám On dal :` (dvojbodka) a delí text na 3 riadky.
  - Jediný slovný rozdiel: `vraví Ježiš sám.` (A, c1 r.2) vs `Vraví Ježiš nám.` (B, v1 r.3).
  - A aj B majú zástupného autora (`...` / `Author Unknown`), takže zlúčenie nič nestratí v tagoch.
- **Čo prevziať z ostatných:**
  - Rozhodnúť `sám`/`nám` (v A je `sám`).
- **Istota:** stredná – Formát hovorí jednoznačne za A, ale správne slovo je neisté.

**Riziká a neistoty:**

- Správne znenie `sám` vs `nám` nie je overené žiadnou referenciou (pieseň nie je v JKS).

---

<a id="g12"></a>
## G12 · [4c] `Bože Otče, teraz vidím (Anonymous).xml` · `Bože Otče, teraz vidím (Chvály).xml`

**Zhrnutie:** Rovnaký text; A má refrén ako samostatnú sloha `c1`, B ho má v `v2` s pokynom `R:` v texte.

**Súbory v skupine:**
- **A** = `Bože Otče, teraz vidím (Anonymous).xml`
- **B** = `Bože Otče, teraz vidím (Chvály).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Bože Otče, teraz vidím` | `Bože Otče, teraz vidím` |
| Tagy (`<author>`) | `Anonymous` | `Chvály` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 c1` | `v1 v2` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 2 / 2 |
| Počet riadkov (neprázdnych) | 6 (6) | 8 (8) |
| Počet slov (bez čísel slôh) | 46 | 47 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 46 | 47 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 2 | 2 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- B v2 r.1: `R: \|: Budem spievať chvály,`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 46 slov v A, 47 slov v B; 1 miest s rozdielom obsahu
1. [pokyn v texte] B v2 r.1: `R:` – v A tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 1, veľkosť písmen: 3, značky opakovania: 1
     - interpunkcia: A v2 r.1 `deti.` vs B v1 r.3 `deti,`
     - veľkosť písmen: A v2 r.2 `Samotu` vs B v1 r.4 `samotu`; A c1 r.1 `budem` vs B v2 r.2 `Budem`; A c1 r.2 `budem` vs B v2 r.3 `Budem`
     - značky opakovania: A c1 r.1 `/:Budem` vs B v2 r.1 `Budem`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v B: `R:`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Anonymous` · tituly: – · text: nič unikátne
- **B**: tagy: `Chvály` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.1: `R:`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Bože Otče, teraz vidím (Anonymous).xml` (A)
- **Zmazať / zlúčiť:** `Bože Otče, teraz vidím (Chvály).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B píše `R: |: Budem spievať chvály,` (v2 r.1) – pokyn `R:` by sa zobrazil na slajde; A má refrén ako `c1` bez pokynu.
  - Rozdiel veľkých písmen: A `Samotu viac nepoznám,` (v2 r.2) vs B `samotu viac nepoznám,` (v1 r.4), A `/:Budem spievať chvály,` vs B `Budem spievať chvály,` (v2 r.2 – refrén začína veľkým písmenom aj mimo začiatku vety).
  - A má dve krátke slohy `v1`, `v2` po 2 riadkoch a samostatný refrén `c1`; B spojila obe slohy do jednej 4-riadkovej `v1` a refrén dala do `v2`.
  - Jediný slovný rozdiel je `R:` – A neobsahuje nič, čo B nemá, okrem štruktúry.
- **Čo prevziať z ostatných:**
  - Z B prevziať tag `Chvály` (a vynechať `Anonymous`); výsledný súbor by sa mal volať «Bože Otče, teraz vidím (Chvály).xml».
- **Istota:** vysoká – Rozdiel je čisto štruktúra.

**Riziká a neistoty:**

- Pri zlúčení sa premenuje A na názov B (rovnaký názov súboru – najprv zmazať B).

---

<a id="g13"></a>
## G13 · [4c] `Čakajú ťa nástrahy (Mariánska).xml` · `Čakajú ťa nástrahy (Anonymous).xml` · `Cakaju ta nastrahy (detsky zbor).xml`

**Zhrnutie:** Rovnaký text; B je najčistejšia (refrén `c1`, bez pokynov), ale nemá `verseOrder`; A a C hrajú refrén po každej slohe.

Existuje aj verzia s akordmi: `Cakaju ta nastrahy (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Čakajú ťa nástrahy (Mariánska).xml`
- **B** = `Čakajú ťa nástrahy (Anonymous).xml`
- **C** = `Cakaju ta nastrahy (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B | C |
|---|---|---|---|
| Zodpovedá konvencii názvu | áno | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | áno / áno | nie / nie | nie / nie |
| Tituly | `Čakajú ťa nástrahy` | `Čakajú ťa nástrahy` | `Cakaju ta nastrahy` |
| Tagy (`<author>`) | `Mariánska` | `Anonymous` | `detsky zbor` |
| songbooks | – | – | – |
| verseOrder | `v1 v2 v3 v2 v4` | – | `v1 c1 v2 c1 v3 c1` |
| copyright / ccliNo | – / – | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4` | `v1 c1 v2 v3` | `v1 v2 v3 c1` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 4 / 4 | 4 / 4 |
| Počet riadkov (neprázdnych) | 14 (14) | 10 (10) | 11 (10) |
| Počet slov (bez čísel slôh) | 87 | 60 | 63 |
| verseOrder vs dokument | líši sa od poradia v dokumente | – | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 113 | 60 | 113 |
| Riadky s číslom slohy na začiatku (`1.`) | 3 | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 | 1 |
| Riadky s koncovou medzerou | 0 | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 4 | 2 | 2 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- A v2 r.1: `R: \|: Mária ma ochraňuje, ja sa nebojím,`
- A v4 r.3: `R: \|: Mária ma ochraňuje, ja sa nebojím,`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica B ↔ A:* 60 slov v B, 87 slov v A; 2 miest s rozdielom obsahu
1. [pokyn v texte] A v2 r.1: `R:` – v B tento text nie je
2. [chýba v B] A v4 r.3–6: `R: Mária ma ochraňuje, ja sa nebojím, vrhnem sa pod jej ochranný plášť. Ona … (26 slov)` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 4, veľkosť písmen: 3, značky opakovania: 1
     - interpunkcia: B v1 r.2 `volá:` vs A v1 r.2 `volá,`; B v1 r.2 `dieťa!”` vs A v1 r.2 `dieťa.`; B v2 r.1 `milosti.` vs A v3 r.1 `milosti,`; B v3 r.1 `milujem.` vs A v4 r.1 `milujem,`
     - veľkosť písmen: B v1 r.2 `“Poď,` vs A v1 r.2 `poď,`; B v2 r.2 `Na` vs A v3 r.2 `na`; B v3 r.2 `Srdce` vs A v4 r.2 `srdce`
     - značky opakovania: B c1 r.4 `najdrahšou.` vs A v2 r.4 `najdrahšou.:\|`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v B: –; viac v A: `a`×1, `ja`×2, `je`×1, `jej`×1, `kráčam`×1, `ma`×1, `Mária`×2, `Matkou`×1, `najdrahšou.`×1, `nebojím,`×1, `ňou,`×1, `ochranný`×1, `ochraňuje,`×1, `Ona`×1, `plášť.`×1, `“Poď,`×1, `podá`×1, `R:`×2, `ruku`×1, `s`×1, `sa`×2, `smelo`×1, `vrhnem`×1
   - V poradí hrania (po rozbalení verseOrder): 60 vs 113 slov, 3 miest s rozdielom obsahu: B `` vs A `R:`; B `` vs A `R: Mária ma ochraňuje, ja sa nebojím, vrhnem … (26 slov)`; B `` vs A `R: Mária ma ochraňuje, ja sa nebojím, vrhnem … (26 slov)`

*Dvojica B ↔ C:* 60 slov v B, 63 slov v C; 1 miest s rozdielom obsahu
3. [rovnaký text na inom mieste (iné poradie slôh)] B v2 r.1 – v3 r.2 a C v1 r.2 – v3 r.2: `Ona nám vždy vyprosí hojné milosti. Na ňu sa spoľahni … (24 slov)`
     - v presunutom úseku: B `` vs C `R.:`
     - v presunutom úseku: B `` vs C `R.:`
     - v presunutom úseku: B `` vs C `R.:`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 2, veľkosť písmen: 1
     - interpunkcia: B v1 r.2 `volá:` vs C v1 r.2 `volá,`; B v1 r.2 `dieťa!”` vs C v1 r.2 `dieťa.`
     - veľkosť písmen: B v1 r.2 `“Poď,` vs C v1 r.2 `poď,`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v B: –; viac v C: `R.:`×3
   - V poradí hrania (po rozbalení verseOrder): 60 vs 113 slov, 3 miest s rozdielom obsahu: B `` vs C `R.:`; B `` vs C `R.: Mária ma ochraňuje, ja sa nebojím, vrhnem … (26 slov)`; B `` vs C `R.: Mária ma ochraňuje, ja sa nebojím, vrhnem … (26 slov)`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Mariánska` · tituly: `Čakajú ťa nástrahy` · text: nič unikátne
- **B**: tagy: `Anonymous` · tituly: `Čakajú ťa nástrahy` · text: nič unikátne
- **C**: tagy: `detsky zbor` · tituly: `Cakaju ta nastrahy` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.2: `R.:`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Čakajú ťa nástrahy (Anonymous).xml` (B)
- **Zmazať / zlúčiť:** `Čakajú ťa nástrahy (Mariánska).xml` (A), `Cakaju ta nastrahy (detsky zbor).xml` (C) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A má refrén vypísaný v `v2` aj v `v4` s pokynmi `R: |:` / `:|`, čísla slôh `1.`/`2.`/`3.` v texte a `verseOrder` `v1 v2 v3 v2 v4`; titul aj názov súboru obsahujú nezlomiteľné medzery.
  - C má na koncoch riadkov pokyn `R.:` (3×), prázdny riadok v `c1` a titul bez diakritiky `Cakaju ta nastrahy`.
  - B má čistý text (`c1` s `/: … :/`, slohy bez čísel), no iba 60 slov, pretože bez `verseOrder` sa refrén zahrá len raz.
  - A aj C hrajú refrén po každej slohe (po rozbalení 113 slov v oboch, rozdiel 0), takže rozumná podoba je B + `verseOrder` `v1 c1 v2 c1 v3 c1`.
- **Čo prevziať z ostatných:**
  - Do B pridať `verseOrder` «v1 c1 v2 c1 v3 c1» (z C).
  - Pridať tagy `Mariánska` (z A) a `detsky zbor` (z C), `Anonymous` vynechať; nový názov «Čakajú ťa nástrahy (Mariánska, detsky zbor).xml».
- **Istota:** stredná – Obsah je rovnaký, rozhodnutie závisí od toho, či sa refrén skutočne spieva po každej slohe (podľa A a C áno).

**Riziká a neistoty:**

- B má typografické úvodzovky `“Poď, moje dieťa!”` a dvojbodku (A, C: `poď, moje dieťa.`); nie je jasné, ktoré je pôvodné.

---

<a id="g14"></a>
## G14 · [4c] `Chválim ťa, Ježiš (Chvály, Večeradlo s Pannou Máriou).xml` · `Chvalim Ta Jezis (detsky zbor).xml`

*Poznámka: `duplicity.md` uvádza pri tejto skupine aj kópie, ktoré už neexistujú (už zlúčené); porovnávané sú len súbory uvedené vyššie.*

**Zhrnutie:** Rovnaký text (37 slov); líši sa poradie hrania: A `c1 v1 v2` bez `verseOrder`, B `c1 v1 c1 v1` a iné rozdelenie slôh.

Existuje aj verzia s akordmi: `Chvalim Ta Jezis (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Chválim ťa, Ježiš (Chvály, Večeradlo s Pannou Máriou).xml`
- **B** = `Chvalim Ta Jezis (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Chválim ťa, Ježiš` | `Chvalim Ta Jezis` |
| Tagy (`<author>`) | `Večeradlo s Pannou Máriou`, `Chvály` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | `c1 v1 c1 v1` |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `c1 v1 v2` | `v1 c1` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 2 / 2 |
| Počet riadkov (neprázdnych) | 8 (8) | 5 (5) |
| Počet slov (bez čísel slôh) | 37 | 37 |
| verseOrder vs dokument | – | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 37 | 74 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 2 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 4 | 3 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | CRLF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- A c1 r.1: `[: Chválim ťa Ježiš :] – 4x`
- B c1 r.1: `Chválim ťa Ježiš:/ 4x`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 37 slov v A, 37 slov v B; 1 miest s rozdielom obsahu
1. [rovnaký text na inom mieste (iné poradie slôh)] A c1 r.1 a B c1 r.1: `Chválim ťa Ježiš 4x`
   - Rozdiely len v zápise (rovnaké slová): značky opakovania: 2, interpunkcia: 2
     - značky opakovania: A v1 r.1 `[:Ani` vs B v1 r.1 `/:Ani`; A v1 r.3 `nás:]` vs B v1 r.2 `nás:/`
     - interpunkcia: A v2 r.2 `tých,` vs B v1 r.3 `tých`; A v2 r.4 `tých,` vs B v1 r.4 `tých`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v B: –
   - V poradí hrania (po rozbalení verseOrder): 37 vs 74 slov, 1 miest s rozdielom obsahu: A `` vs B `Chválim ťa Ježiš:/ 4x /:Ani oko nevidelo, ani … (37 slov)`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Chvály`, `Večeradlo s Pannou Máriou` · tituly: `Chválim ťa, Ježiš` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1: `Chválim ťa Ježiš 4x`
- **B**: tagy: `detsky zbor` · tituly: `Chvalim Ta Jezis` · verseOrder `c1 v1 c1 v1` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1: `Chválim ťa Ježiš:/ 4x`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Chválim ťa, Ježiš (Chvály, Večeradlo s Pannou Máriou).xml` (A)
- **Zmazať / zlúčiť:** `Chvalim Ta Jezis (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Slovo po slove sú súbory totožné; rozdiel je len v rozdelení: A má 3 slohy (`c1`, `v1`, `v2`), B 2 slohy (`v1` so 4 riadkami, `c1`).
  - A má správne uzavreté značky opakovania `[: … :]`; B má pri refréne iba koncovú značku `Chválim ťa Ježiš:/ 4x` bez otvárajúcej `/:`.
  - A má špecifickejšie tagy (`Večeradlo s Pannou Máriou`, `Chvály`), B len `detsky zbor`; A má pokyn `– 4x` v texte (aj B: `4x`).
  - Hrací poriadok B `c1 v1 c1 v1` (po rozbalení 74 slov) by zobrazil celú slohu `v1` dvakrát; poradie v A `c1 v1 v2` sa spievaním nemusí zhodovať.
- **Čo prevziať z ostatných:**
  - Pridať tag `detsky zbor`; rozhodnúť, či po slohách 1–2 sa refrén opakuje (potom `verseOrder` v A «c1 v1 v2 c1»).
- **Istota:** stredná – Text je rovnaký, ale poradie hrania nie je z dát zistiteľné.

**Riziká a neistoty:**

- Poradie spevu refrénu sa nedá overiť; zmazanie B stratí len jej `verseOrder`.

---

<a id="g15"></a>
## G15 · [4c] `Dávam všetko (Adorácia, Obetné dary, Rieka života).xml` · `Dávam všetko (...).xml` · `Dnes chcel by som ti dať (Rieka Života).xml` · `Dnes chcel by som Ti dat (detsky zbor).xml`

**Zhrnutie:** Štyri kópie tej istej piesne; B má čistý text a refrén ako `c1`/`c2` po každej polovici, A má `R:` v texte, C preklep `právd.`, D natiahnutú slabiku `dá -á-vam`.

Existuje aj verzia s akordmi: `Dnes chcel by som Ti dat (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Dávam všetko (Adorácia, Obetné dary, Rieka života).xml`
- **B** = `Dávam všetko (...).xml`
- **C** = `Dnes chcel by som ti dať (Rieka Života).xml`
- **D** = `Dnes chcel by som Ti dat (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B | C | D |
|---|---|---|---|---|
| Zodpovedá konvencii názvu | áno | áno | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie | nie / nie | nie / nie |
| Tituly | `Dávam všetko` | `Dávam všetko` | `Dnes chcel by som ti dať` | `Dnes chcel by som Ti dat` |
| Tagy (`<author>`) | `Adorácia`, `Obetné dary`, `Rieka života` | `...` | `Rieka Života` | `detsky zbor` |
| songbooks | – | – | – | – |
| verseOrder | – | – | – | `v1 c1 v2 c1` |
| copyright / ccliNo | – / – | – / – | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3` | `v1 o1 c1 v2 o2 c2` | `v1 v2 c1 v3 v4` | `v1 v2 c1` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 6 / 6 | 5 / 5 | 3 / 3 |
| Počet riadkov (neprázdnych) | 10 (10) | 10 (10) | 18 (18) | 11 (9) |
| Počet slov (bez čísel slôh) | 84 | 83 | 74 | 76 |
| verseOrder vs dokument | – | – | – | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 84 | 83 | 74 | 85 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 | 0 | 2 |
| Riadky s koncovou medzerou | 0 | 0 | 1 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 | 1 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 4 | 0 | 2 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- A v2 r.1: `R: A dávam všetko, to, čo mám, Tebe Kráľ.`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica B ↔ A:* 83 slov v B, 84 slov v A; 1 miest s rozdielom obsahu
1. [rovnaký text na inom mieste (iné poradie slôh)] B c2 r.1 a A v2 r.1: `A dávam všetko, to čo mám, Tebe, Kráľ.`
     - v presunutom úseku: B `` vs A `R:`
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 2, interpunkcia: 2
     - veľkosť písmen: B v1 r.1 `Ti` vs A v1 r.1 `ti`; B v1 r.2 `Tvojim` vs A v1 r.2 `tvojim`
     - interpunkcia: B c1 r.1 `to` vs A v2 r.2 `to,`; B c1 r.1 `Tebe,` vs A v2 r.2 `Tebe`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v B: –; viac v A: `R:`×1
   - V poradí hrania (po rozbalení verseOrder): 83 vs 84 slov, 1 miest s rozdielom obsahu: B `A dávam všetko, to čo mám, Tebe, Kráľ.` vs A `R: A dávam všetko, to, čo mám, Tebe … (9 slov)`

*Dvojica B ↔ C:* 83 slov v B, 74 slov v C; 3 miest s rozdielom obsahu
2. [preklep / zmena slova] B o1 r.1: `práv,`  vs  C v2 r.2: `právd.`
     - riadok v B: `dnes kladiem svoje sny, ja sa zriekam svojich práv,`
     - riadok v C: `ja sa zriekam svojich právd.`
3. [chýba v C] B c1 r.1: `A` – v C tento text nie je
4. [chýba v C] B c2 r.1: `A dávam všetko, to čo mám, Tebe, Kráľ.` – v C tento text nie je
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 12, interpunkcia: 10
     - veľkosť písmen: B v1 r.1 `Ti` vs C v1 r.1 `ti`; B v1 r.2 `dávam` vs C v1 r.3 `Dávam`; B v1 r.2 `Tvojim` vs C v1 r.4 `tvojim`; B o1 r.1 `dnes` vs C v2 r.1 `Dnes`; B o1 r.2 `už` vs C v2 r.3 `Už`; B c1 r.1 `dávam` vs C c1 r.1 `Dávam`; B c1 r.1 `Tebe,` vs C c1 r.2 `tebe,`; B v2 r.2 `a` vs C v3 r.3 `A` … (+4)
     - interpunkcia: B v1 r.1 `mám,` vs C v1 r.2 `mám`; B v1 r.2 `Kráľ,` vs C v1 r.4 `Kráľ`; B c1 r.1 `všetko,` vs C c1 r.1 `všetko`; B c1 r.1 `to` vs C c1 r.2 `to,`; B c1 r.1 `mám,` vs C c1 r.2 `mám`; B c1 r.1 `Kráľ.` vs C c1 r.2 `Kráľ`; B v2 r.1 `sám` vs C v3 r.2 `sám.`; B v2 r.2 `bohatstvá` vs C v3 r.3 `bohatstvá,` … (+2)
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v B: `A`×2, `čo`×1, `dávam`×1, `Kráľ,`×1, `mám,`×1, `práv,`×1, `Tebe,`×1, `to,`×1, `všetko,`×1; viac v C: `právd.`×1
   - V poradí hrania (po rozbalení verseOrder): 83 vs 74 slov, 3 miest s rozdielom obsahu: B `práv,` vs C `právd.`; B `A` vs C ``; B `A dávam všetko, to čo mám, Tebe, Kráľ.` vs C ``

*Dvojica B ↔ D:* 83 slov v B, 76 slov v D; 2 miest s rozdielom obsahu
5. [chýba v D] B c1 r.1: `A dávam všetko, to čo mám, Tebe, Kráľ.` – v D tento text nie je
6. [preklep / zmena slova] B c2 r.1: `dávam`  vs  D c1 r.1: `dá -á-vam`
     - riadok v B: `[: A dávam všetko, to čo mám, Tebe, Kráľ. :]`
     - riadok v D: `/: A dá -á-vam všetko, to čo mám, Tebe, kráľ.:/`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 6, veľkosť písmen: 4
     - interpunkcia: B v1 r.1 `mám,` vs D v1 r.1 `mám.`; B v1 r.2 `nohám,` vs D v1 r.2 `nohám`; B v1 r.2 `Kráľ,` vs D v1 r.2 `Kráľ.`; B o1 r.2 `mať.` vs D v1 r.5 `mať...`; B v2 r.2 `pokladám,` vs D v2 r.2 `pokladám.`; B o2 r.2 `mám.` vs D v2 r.5 `mám...`
     - veľkosť písmen: B v1 r.2 `dávam` vs D v1 r.2 `Dávam`; B o1 r.1 `dnes` vs D v1 r.4 `Dnes`; B o2 r.1 `chcem` vs D v2 r.4 `Chcem`; B c2 r.1 `Kráľ.` vs D c1 r.1 `kráľ.:/`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v B: `A`×1, `čo`×1, `dávam`×2, `Kráľ,`×1, `mám,`×1, `Tebe,`×1, `to,`×1, `všetko,`×1; viac v D: `-á-vam`×1, `dá`×1
   - V poradí hrania (po rozbalení verseOrder): 83 vs 85 slov, 2 miest s rozdielom obsahu: B `dávam` vs D `dá -á-vam`; B `dávam` vs D `dá -á-vam`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Adorácia`, `Obetné dary`, `Rieka života` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.1: `R: A dávam všetko, to, čo mám, Tebe Kráľ.`
- **B**: tagy: `...` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): c2 r.1: `dávam`
- **C**: tagy: `Rieka Života` · tituly: `Dnes chcel by som ti dať` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.2: `právd.`
- **D**: tagy: `detsky zbor` · tituly: `Dnes chcel by som Ti dat` · verseOrder `v1 c1 v2 c1` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1: `dá -á-vam`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Dávam všetko (...).xml` (B)
- **Zmazať / zlúčiť:** `Dávam všetko (Adorácia, Obetné dary, Rieka života).xml` (A), `Dnes chcel by som ti dať (Rieka Života).xml` (C), `Dnes chcel by som Ti dat (detsky zbor).xml` (D) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A: refrén je v `v2` s pokynom `R: A dávam všetko, to, čo mám, Tebe Kráľ.` a ešte raz bez `R:`; chýba `verseOrder`, takže refrén zaznie iba raz (po v1).
  - C: preklep `právd.` (v2 r.2) – A, B aj D majú `práv`; refrén má iný text (`Dávam všetko to, čo mám tebe, Kráľ`) a zaznie podľa dokumentu iba raz.
  - D: `A dá -á-vam všetko, to čo mám, Tebe, kráľ.:/` (c1 r.1) – natiahnutá slabika a malé „kráľ“; trojbodky `mať...`, `mám...` a prázdny riadok v každej slohe.
  - B hrá refrén po každej polovici slohy (`v1 o1 c1 v2 o2 c2`) bez `verseOrder` a bez preklepov; tag v B je zástupný `...`.
- **Čo prevziať z ostatných:**
  - Z A prevziať tagy `Adorácia`, `Obetné dary`, `Rieka života`; z C tag `Rieka Života` a titul `Dnes chcel by som ti dať` (ako druhý `<title>`); tag `...` vynechať.
  - Tag je v dátach 7× `Rieka Života` a 1× `Rieka života` – zjednotiť.
- **Istota:** stredná – Text je rovnaký, ale výber štruktúry (`o1`/`o2` v B vs `v1`/`v2` + `c1` v D) je vecou vkusu.

**Riziká a neistoty:**

- B používa typ slohy `o1`/`o2` (other) – vyzerá neštandardne, ale funguje.
- Rôzne delenie slôh na slajdy (2+2 riadky v B, 4 riadky v A, 5 riadkov v D).

---

<a id="g16"></a>
## G16 · [4c] `Do tmy našich dní (Advent, Pomalá, Pôstna, Taize).xml` · `Do tmy našich dní (Taize).xml`

**Zhrnutie:** B je presne druhá polovica A (14 z 28 slov) a jej jediný tag `Taize` má aj A.

**Súbory v skupine:**
- **A** = `Do tmy našich dní (Advent, Pomalá, Pôstna, Taize).xml`
- **B** = `Do tmy našich dní (Taize).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Do tmy našich dní` | `Do tmy našich dní` |
| Tagy (`<author>`) | `Advent`, `Pôstna`, `Pomalá`, `Taize` | `Taize` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1` | `v1` |
| Počet slôh / `<lines>` blokov | 1 / 1 | 1 / 1 |
| Počet riadkov (neprázdnych) | 8 (8) | 2 (2) |
| Počet slov (bez čísel slôh) | 28 | 14 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 28 | 14 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 1 |
| Riadky s dvojitou medzerou vnútri | 0 | 1 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 28 slov v A, 14 slov v B; 1 miest s rozdielom obsahu
1. [chýba v B] A v1 r.1–4: `Do tmy našich dní nám dávaš svoj oheň, ktorý viac nezhasne, ktorý viac nezhasne.` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 1
     - interpunkcia: A v1 r.5 `dní` vs B v1 r.1 `dní,`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `dávaš`×1, `dní`×1, `Do`×1, `ktorý`×2, `nám`×1, `našich`×1, `nezhasne,`×2, `oheň,`×1, `svoj`×1, `tmy`×1, `viac`×2; viac v B: –

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Advent`, `Pomalá`, `Pôstna` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1–4: `Do tmy našich dní nám dávaš svoj oheň, ktorý viac nezhasne, ktorý viac nezhasne.`
- **B**: tagy: – · tituly: – · text: nič unikátne

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Do tmy našich dní (Advent, Pomalá, Pôstna, Taize).xml` (A)
- **Zmazať / zlúčiť:** `Do tmy našich dní (Taize).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A má text vypísaný dvakrát (8 riadkov); B má len 2 riadky `Do tmy našich dní, nám dávaš svoj oheň,` / `ktorý viac nezhasne, ktorý nikdy nezhasne.`, čo je slovo po slove druhá polovica A (v1 r.5–8).
  - A má všetky tagy B (`Taize`) a navyše `Advent`, `Pomalá`, `Pôstna`.
  - B nemá žiadny unikátny text, titul ani tag.
- **Čo prevziať z ostatných:** nič.
- **Istota:** vysoká – B je podmnožina A v texte aj v tagoch.

**Riziká a neistoty:**

- A zobrazí na slajde 8 riadkov so stále sa opakujúcim textom; ak je to príliš dlhé, treba A rozdeliť na dve slohy (netýka sa zmazania B).

---

<a id="g17"></a>
## G17 · [4c] `Dobrorečíme Ti (Obetné dary).xml` · `Dobrorecime Ti (detsky zbor).xml`

**Zhrnutie:** Rovnaký text; B má refrén ako `c1` + `verseOrder` (lepšia štruktúra) a jeden preklep `ako ako`, A má refrén vpísaný do oboch slôh a čísla slôh na samostatnom riadku.

**Súbory v skupine:**
- **A** = `Dobrorečíme Ti (Obetné dary).xml`
- **B** = `Dobrorecime Ti (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Dobrorečíme Ti` | `Dobrorecime Ti` |
| Tagy (`<author>`) | `Obetné dary` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | `v1 c1 v2 c1` |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2` | `v1 v2 c1` |
| Počet slôh / `<lines>` blokov | 2 / 2 | 3 / 3 |
| Počet riadkov (neprázdnych) | 16 (16) | 8 (8) |
| Počet slov (bez čísel slôh) | 72 | 66 |
| verseOrder vs dokument | – | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 72 | 73 |
| Riadky s číslom slohy na začiatku (`1.`) | 2 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 2 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 4 | 2 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica B ↔ A:* 66 slov v B, 72 slov v A; 2 miest s rozdielom obsahu
1. [chýba v A (opakovanie vypísané v B)] B v1 r.3: `ako` – v A tento text nie je
2. [chýba v B] A v1 r.7–8: `Zvelebený Boh, zvelebený Boh, zvelebený Boh naveky.` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 6, značky opakovania: 1
     - veľkosť písmen: B v1 r.1 `ti,` vs A v1 r.2 `Ti,`; B v1 r.2 `tvojej` vs A v1 r.3 `Tvojej`; B v1 r.3 `tebe` vs A v1 r.4 `Tebe`; B v2 r.1 `ti,` vs A v2 r.2 `Ti,`; B v2 r.2 `tvojej` vs A v2 r.3 `Tvojej`; B v2 r.3 `tebe` vs A v2 r.4 `Tebe`
     - značky opakovania: B c1 r.1 `/:Zvelebený` vs A v2 r.7 `Zvelebený`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v B: `ako`×1; viac v A: `Boh,`×3, `naveky.`×1, `/:Zvelebený`×3
   - V poradí hrania (po rozbalení verseOrder): 73 vs 72 slov, 1 miest s rozdielom obsahu: B `ako` vs A ``

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Obetné dary` · tituly: `Dobrorečíme Ti` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.7–8: `Zvelebený Boh, zvelebený Boh, zvelebený Boh naveky.`
- **B**: tagy: `detsky zbor` · tituly: `Dobrorecime Ti` · verseOrder `v1 c1 v2 c1` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.3: `ako`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Dobrorecime Ti (detsky zbor).xml` (B)
- **Zmazať / zlúčiť:** `Dobrorečíme Ti (Obetné dary).xml` (A) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Jediný slovný rozdiel: `ako ako plod zeme` (B, v1 r.3) – preklep, A má `ako plod zeme`.
  - A má refrén `|: Zvelebený Boh, zvelebený Boh,` … `zvelebený Boh naveky. :|` vypísaný v oboch slohách a samostatný riadok `1. ` / `2. ` v každej; B ho má raz ako `c1` a hrá ho cez `verseOrder` `v1 c1 v2 c1` (po rozbalení sa líši len o `ako`).
  - A píše zvratné zámená veľkým (`Ti`, `Tvojej`, `Tebe`), B malým (`ti`, `tvojej`, `tebe`); A má titul s diakritikou `Dobrorečíme Ti`, B `Dobrorecime Ti`.
  - B má dlhé riadky (v1 r.3 má 17 slov), A rozdeľuje text na krátke riadky.
- **Čo prevziať z ostatných:**
  - V B opraviť `ako ako` → `ako`, titul na `Dobrorečíme Ti`, pridať tag `Obetné dary`.
  - Rozhodnúť o veľkých písmenách `Ti`/`Tvojej`/`Tebe` (A) a prípadne rozdeliť dlhé riadky podľa A.
- **Istota:** stredná – Text je rovnaký; rozhodnutie je medzi štruktúrou B a kvalitou riadkovania A.

**Riziká a neistoty:**

- Veľké/malé písmená zámen pre Boha sú vec štýlu zboru.

---

<a id="g18"></a>
## G18 · [4c] `Glória - UPC (Glória).xml` · `Gloria_Vinbarg (detsky zbor).xml`

**Zhrnutie:** Rovnaký text; A má správne `excelsis`, ale pokyn `R:` a chýba mu `verseOrder`; B má `verseOrder`, ale preklep `exelsis`.

Existuje aj verzia s akordmi: `Gloria_Vinbarg (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Glória - UPC (Glória).xml`
- **B** = `Gloria_Vinbarg (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Glória - UPC` | `Gloria_Vinbarg` |
| Tagy (`<author>`) | `Glória` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | `c1 v1 c1 v2 c1 v3 c1` |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4` | `v1 v2 v3 c1` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 4 / 4 |
| Počet riadkov (neprázdnych) | 10 (10) | 15 (15) |
| Počet slov (bez čísel slôh) | 57 | 56 |
| verseOrder vs dokument | – | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 57 | 71 |
| Riadky s číslom slohy na začiatku (`1.`) | 3 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 2 | 2 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | CRLF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- A v1 r.1: `R: \|: Glória, glória, in excelsis deo :\|`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 57 slov v A, 56 slov v B; 2 miest s rozdielom obsahu
1. [rovnaký text na inom mieste (iné poradie slôh)] A v1 r.1 a B c1 r.1: `R: Glória, glória, in excelsis deo`
     - v presunutom úseku: A `R:` vs B ``
     - v presunutom úseku: A `excelsis` vs B `exelsis`
2. [preklep / zmena slova] A v3 r.3: `pokorné.`  vs  B v2 r.5: `pokorné-é.`
     - riadok v A: `prijmi prosby pokorné.`
     - riadok v B: `prijmi prosby pokorné-é.`
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 5, interpunkcia: 4
     - veľkosť písmen: A v2 r.1 `Zemi.` vs B v1 r.2 `zemi,`; A v2 r.2 `My` vs B v1 r.3 `my`; A v3 r.1 `spasiteľ` vs B v2 r.1 `Spasiteľ`; A v4 r.2 `ty` vs B v3 r.3 `Ty`; A v4 r.3 `AMEN.` vs B v3 r.4 `Amen.`
     - interpunkcia: A v2 r.3 `sláva` vs B v1 r.5 `sláva!`; A v3 r.1 `Ježiš` vs B v2 r.1 `Ježiš,`; A v4 r.2 `Duchom,` vs B v3 r.3 `Duchom`; A v4 r.3 `Otca` vs B v3 r.4 `Otca.`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `excelsis`×1, `pokorné.`×1, `R:`×1; viac v B: `exelsis`×1, `pokorné-é.`×1
   - V poradí hrania (po rozbalení verseOrder): 57 vs 71 slov, 5 miest s rozdielom obsahu: A `R:` vs B ``; A `excelsis` vs B `exelsis`; A `` vs B `/:Glória, glória, in exelsis deo!`; A `pokorné.` vs B `pokorné-é. /:Glória, glória, in exelsis deo!`; A `` vs B `/:Glória, glória, in exelsis deo!`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Glória` · tituly: `Glória - UPC` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1: `R: Glória, glória, in excelsis deo`; v3 r.3: `pokorné.`
- **B**: tagy: `detsky zbor` · tituly: `Gloria_Vinbarg` · verseOrder `c1 v1 c1 v2 c1 v3 c1` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.5: `pokorné-é.`; c1 r.1: `/:Glória, glória, in exelsis deo!`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Glória - UPC (Glória).xml` (A)
- **Zmazať / zlúčiť:** `Gloria_Vinbarg (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B má v refréne preklep v latinčine: `Glória, glória, in exelsis deo!` (c1 r.1); A má `in excelsis deo`.
  - A ukladá refrén ako prvú slohu `v1` s pokynom `R: |: Glória, glória, in excelsis deo :|` (pokyn `R:` sa zobrazí na slajde) a nemá `verseOrder`, takže refrén zaznie iba raz na začiatku.
  - B hrá refrén pred každou slohou (`verseOrder` `c1 v1 c1 v2 c1 v3 c1`, po rozbalení 71 slov oproti 57 v A).
  - B má natiahnutú slabiku `pokorné-é.` (v2 r.5), A `pokorné.`; A má čísla slôh `1.`, `2.`, `3.` v textových riadkoch a `AMEN.` veľkými písmenami, B `Amen.`.
- **Čo prevziať z ostatných:**
  - Do A pridať `verseOrder` «v1 v2 v1 v3 v1 v4 v1» (zodpovedá poradiu `c1 v1 c1 v2 c1 v3 c1` v B) a odstrániť pokyn `R:`.
  - Pridať tag `detsky zbor`; titul `Gloria_Vinbarg` z B voliteľne ako druhý titul.
- **Istota:** stredná – Obsah je rovnaký, rozhodnutie je medzi správnym znením (A) a hotovým poradím hrania (B).

**Riziká a neistoty:**

- Poradie hrania refrénu je prevzaté z B a nedá sa overiť.

---

<a id="g19"></a>
## G19 · [4c] `Jasaj v Pánovi celá Zem (Veľkonočná).xml` · `Jasaj v Pánovi (Anonymous).xml`

**Zhrnutie:** Slohy majú rovnaký text, ale refrén sa líši (A: `Jasaj (jasaj, jasaj) v Pánovi (v Pánovi)` po každej sloha a `Záver:`, B: jedna veta `Jasaj v Pánovi, jasaj v Pánovi.`).

**Súbory v skupine:**
- **A** = `Jasaj v Pánovi celá Zem (Veľkonočná).xml`
- **B** = `Jasaj v Pánovi (Anonymous).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Jasaj v Pánovi celá Zem` | `Jasaj v Pánovi` |
| Tagy (`<author>`) | `Veľkonočná` | `Anonymous` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4` | `v1 c1 v2 v3` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 4 / 4 |
| Počet riadkov (neprázdnych) | 11 (11) | 7 (7) |
| Počet slov (bez čísel slôh) | 62 | 38 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 62 | 38 |
| Riadky s číslom slohy na začiatku (`1.`) | 3 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 12 | 6 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- A v1 r.3: `R: \|: Jasaj (jasaj, jasaj) v Pánovi (v Pánovi) :\|`
- A v2 r.3: `R: \|: Jasaj (jasaj, jasaj) v Pánovi (v Pánovi) :\|`
- A v3 r.3: `R: \|: Jasaj (jasaj, jasaj) v Pánovi (v Pánovi) :\|`
- A v4 r.1: `Záver:`
- A v1 r.3 (zátvorka): `(jasaj, jasaj)`
- A v1 r.3 (zátvorka): `(v Pánovi)`
- A v2 r.3 (zátvorka): `(jasaj, jasaj)`
- A v2 r.3 (zátvorka): `(v Pánovi)`
- A v3 r.3 (zátvorka): `(jasaj, jasaj)`
- A v3 r.3 (zátvorka): `(v Pánovi)`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 62 slov v A, 38 slov v B; 4 miest s rozdielom obsahu
1. [chýba v B] A v1 r.3: `R: Jasaj (jasaj,` – v B tento text nie je
2. [chýba v A] B c1 r.1: `jasaj` – v A tento text nie je
3. [chýba v B] A v2 r.3: `R: Jasaj (jasaj, jasaj) v Pánovi (v Pánovi)` – v B tento text nie je
4. [chýba v B] A v3 r.3 – v4 r.2: `R: Jasaj (jasaj, jasaj) v Pánovi (v Pánovi) Záver: Jasaj v Pánovi celá Zem,` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 4, interpunkcia: 5
     - veľkosť písmen: A v1 r.1 `Zem,` vs B v1 r.1 `zem,`; A v1 r.3 `jasaj)` vs B c1 r.1 `Jasaj`; A v3 r.1 `On` vs B v3 r.1 `on`; A v3 r.2 `On` vs B v3 r.2 `on`
     - interpunkcia: A v1 r.2 `deň` vs B v1 r.2 `deň.`; A v1 r.3 `Pánovi` vs B c1 r.1 `Pánovi,`; A v1 r.3 `(v` vs B c1 r.1 `v`; A v1 r.3 `Pánovi)` vs B c1 r.1 `Pánovi.`; A v3 r.1 `Pána,` vs B v3 r.1 `Pána`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `celá`×1, `Jasaj`×8, `Pánovi`×5, `R:`×3, `v`×5, `Záver:`×1, `Zem,`×1; viac v B: –

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Veľkonočná` · tituly: `Jasaj v Pánovi celá Zem` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.3: `R: Jasaj (jasaj,`; v2 r.3: `R: Jasaj (jasaj, jasaj) v Pánovi (v Pánovi)`; v3 r.3 – v4 r.2: `R: Jasaj (jasaj, jasaj) v Pánovi (v Pánovi) Záver: Jasaj v Pánovi celá Zem,`
- **B**: tagy: `Anonymous` · tituly: `Jasaj v Pánovi` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1: `jasaj`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Jasaj v Pánovi celá Zem (Veľkonočná).xml` (A)
- **Zmazať / zlúčiť:** `Jasaj v Pánovi (Anonymous).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A má 62 slov, B 38; A navyše obsahuje refrén po každej z 3 slôh (`R: |: Jasaj (jasaj, jasaj) v Pánovi (v Pánovi) :|`) a záver (v4: `Záver:` / `Jasaj v Pánovi celá Zem,`), ktoré B nemá.
  - B má refrén ako `c1` s inou podobou: `Jasaj v Pánovi, jasaj v Pánovi.`; nemá `verseOrder`, takže refrén zaznie raz (po v1).
  - Slová slôh sú rovnaké (napr. `toto je veľký Hospodinov deň` v oboch), líši sa interpunkcia (`zem,`/`Zem,`, `on`/`On`).
  - A má pokyny `R:` a `Záver:` v texte (zobrazia sa na slajde) a čísla `1.`, `2.`, `3.` v riadkoch; tag `Veľkonočná` je reálny, v B len `Anonymous`.
- **Čo prevziať z ostatných:**
  - Z B prevziať nič; ak sa nájde správna podoba refrénu, upraviť v A.
- **Istota:** stredná – A je úplnejšia, ale nedá sa zistiť, ktorý refrén je správny.

**Riziká a neistoty:**

- Ktorú podobu refrénu zbor spieva, nie je z dát zistiteľné.
- Záver v4 má v A iba jeden riadok `Jasaj v Pánovi celá Zem,` (možno nedokončený).

---

<a id="g20"></a>
## G20 · [4c] `Ježiš môj (Anonymous).xml` · `Jezis moj, pred tvojou stojim obetou (detsky zbor).xml`

**Zhrnutie:** Rovnaký text; A vypisuje opakovania a má `Mnoho krát`, B ich zapisuje značkami `/: :/`, má `verseOrder` a `mnohokrát`.

Existuje aj verzia s akordmi: `Jezis moj, pred tvojou stojim obetou (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Ježiš môj (Anonymous).xml`
- **B** = `Jezis moj, pred tvojou stojim obetou (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Ježiš môj` | `Jezis moj, pred tvojou stojim obetou` |
| Tagy (`<author>`) | `Anonymous` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | `v1 c1 v2 c1 c2` |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4 v5 v6 c1` | `v1 v2 c1 c2` |
| Počet slôh / `<lines>` blokov | 7 / 7 | 4 / 4 |
| Počet riadkov (neprázdnych) | 24 (24) | 13 (13) |
| Počet slov (bez čísel slôh) | 101 | 90 |
| verseOrder vs dokument | – | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 101 | 114 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 1 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 8 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | CRLF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica B ↔ A:* 90 slov v B, 101 slov v A; 4 miest s rozdielom obsahu
1. [preklep / zmena slova] B v1 r.3: `mnohokrát`  vs  A v2 r.1: `Mnoho krát`
     - riadok v B: `mnohokrát ja žasnem ako máš nás rád`
     - riadok v A: `Mnoho krát ja žasnem`
2. [chýba v B] A v2 r.4 – v4 r.2: `stojím tu dnes ešte raz. A znova hľadím na kríž kde si svoj život … (29 slov)` – v B tento text nie je
3. [iný text] B c1 r.1–3: `A znova hľadím na kríž kde si svoj život dal, som pokorený láskou srdce … (18 slov)`  vs  A v6 r.4: `chválu`
4. [iný text] B c1 r.3: `ďakujem svoj život Ti dám.`  vs  A v6 r.4: `vzdám ešte raz`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 7, značky opakovania: 3, veľkosť písmen: 4
     - interpunkcia: B v1 r.1 `obetou,` vs A v1 r.1 `obetou`; B v1 r.2 `šiel,` vs A v1 r.2 `šiel`; B v2 r.1 `nebi,` vs A v5 r.2 `nebi`; B v2 r.2 `stáť,` vs A v5 r.4 `stáť`; B c2 r.1 `kríž,` vs A c1 r.1 `kríž`; B c2 r.1 `kríž,` vs A c1 r.2 `kríž`; B c2 r.2 `môj.` vs A c1 r.4 `môj`
     - značky opakovania: B v1 r.4 `/:stojím` vs A v2 r.3 `stojím`; B v2 r.4 `/:chválu` vs A v6 r.3 `chválu`; B v2 r.4 `raz:/` vs A v6 r.3 `raz`
     - veľkosť písmen: B v2 r.3 `teraz` vs A v6 r.1 `Teraz`; B v2 r.4 `Ti` vs A v6 r.3 `ti`; B c1 r.3 `Ti,` vs A v6 r.4 `ti`; B c2 r.2 `vďaka` vs A c1 r.3 `Vďaka`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v B: `mnohokrát`×1; viac v A: `/:chválu`×1, `dnes`×1, `ešte`×2, `krát`×1, `Mnoho`×1, `raz`×2, `stojím`×1, `Ti`×1, `tu`×1, `vzdám`×1
   - V poradí hrania (po rozbalení verseOrder): 114 vs 101 slov, 4 miest s rozdielom obsahu: B `mnohokrát` vs A `Mnoho krát`; B `` vs A `stojím tu dnes ešte raz`; B `A znova hľadím na kríž kde si svoj … (18 slov)` vs A `chválu`; B `ďakujem svoj život Ti dám.` vs A `vzdám ešte raz`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Anonymous` · tituly: `Ježiš môj` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.1: `Mnoho krát`; v2 r.4: `stojím`; v2 r.4: `dnes`; v5 r.1 – v6 r.4: `Najvyšší si teraz Ježiš na nebi nebeský vládca raz budem tam stáť Teraz však tu žasnem … (31 slov)`
- **B**: tagy: `detsky zbor` · tituly: `Jezis moj, pred tvojou stojim obetou` · verseOrder `v1 c1 v2 c1 c2` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.3: `mnohokrát`; c1 r.1–3: `A znova hľadím na kríž kde si svoj život dal, som pokorený láskou srdce zlomené mám, … (18 slov)`; c1 r.3: `ďakujem svoj život Ti dám.`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Jezis moj, pred tvojou stojim obetou (detsky zbor).xml` (B)
- **Zmazať / zlúčiť:** `Ježiš môj (Anonymous).xml` (A) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Rozdiel 11 slov v A tvorí vypísané opakovanie (`stojím tu dnes ešte raz` 2×, `chválu ti vzdám ešte raz` 2×) a rozdelené `Mnoho krát` (A, v2 r.1); B má `mnohokrát` a opakovania ako `a /:stojím tu dnes ešte raz :/` (v1 r.4) a `a /:chválu Ti vzdám ešte raz:/` (v2 r.4).
  - B má `verseOrder` `v1 c1 v2 c1 c2`, takže pasáž `A znova hľadím na kríž …` zaznie aj po 2. sloha; A nemá `verseOrder`, zaznie raz (po rozbalení 101 vs 114 slov).
  - B má 13 riadkov v 4 slohách (dlhšie riadky), A 24 riadkov v 7 slohách (krátke riadky).
  - B má titul bez diakritiky `Jezis moj, pred tvojou stojim obetou`; A má `Ježiš môj`; tag A je zástupný `Anonymous`.
- **Čo prevziať z ostatných:**
  - Titul B opraviť na «Ježiš môj, pred tvojou stojím obetou» a pridať druhý titul `Ježiš môj`.
- **Istota:** stredná – Obsah je rovnaký; voľba medzi krátkymi riadkami (A) a kompaktnou štruktúrou so `verseOrder` (B).

**Riziká a neistoty:**

- Kapitálky `Ti`/`ti` sa v oboch líšia (štýl).

---

<a id="g21"></a>
## G21 · [4c] `Ježiš, ty si skalou (Prijímanie).xml` · `Ježiš, ty si skalou (Anonymous).xml` · `Jezis ty si skalou (detsky zbor).xml`

**Zhrnutie:** Rovnaký text (33 slov) v A a B; C pridáva pokyny `R:` a má obe slohy v jednej sloha.

**Súbory v skupine:**
- **A** = `Ježiš, ty si skalou (Prijímanie).xml`
- **B** = `Ježiš, ty si skalou (Anonymous).xml`
- **C** = `Jezis ty si skalou (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B | C |
|---|---|---|---|
| Zodpovedá konvencii názvu | áno | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie | nie / nie |
| Tituly | `Ježiš, ty si skalou` | `Ježiš, ty si skalou` | `Jezis ty si skalou` |
| Tagy (`<author>`) | `Prijímanie` | `Anonymous` | `detsky zbor` |
| songbooks | – | – | – |
| verseOrder | – | – | – |
| copyright / ccliNo | – / – | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2` | `v1 v2` | `v1` |
| Počet slôh / `<lines>` blokov | 2 / 2 | 2 / 2 | 1 / 1 |
| Počet riadkov (neprázdnych) | 10 (10) | 11 (10) | 6 (6) |
| Počet slov (bez čísel slôh) | 33 | 33 | 35 |
| verseOrder vs dokument | – | – | – |
| Slov po rozbalení verseOrder | 33 | 33 | 35 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 | 2 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 1 | 0 |
| Riadky s koncovou medzerou | 0 | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 | 1 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 8 | 20 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- C v1 r.3: `R: Aleluja, mojím štítom si.`
- C v1 r.6: `R: Aleluja, dôverujem ti`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 33 slov v A, 33 slov v B; obsah slov (po zložení diakritiky/veľkosti/interpunkcie) je **rovnaký**
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 1, interpunkcia: 2
     - veľkosť písmen: A v1 r.1 `Skalou,` vs B v1 r.1 `skalou,`
     - interpunkcia: A v1 r.5 `A-le-lu-ja,` vs B v1 r.5 `A-le-lu-ja`; A v2 r.5 `A-le-lu-ja,` vs B v2 r.5 `Aleluja,`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v B: –

*Dvojica A ↔ C:* 33 slov v A, 35 slov v C; 2 miest s rozdielom obsahu
1. [pokyn v texte] C v1 r.3: `R:` – v A tento text nie je
2. [pokyn v texte] C v1 r.6: `R:` – v A tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 5, veľkosť písmen: 7
     - interpunkcia: A v1 r.1 `Ježiš,` vs C v1 r.1 `Ježiš`; A v1 r.5 `A-le-lu-ja,` vs C v1 r.3 `Aleluja,`; A v2 r.1 `Ježiš,` vs C v1 r.4 `Ježiš`; A v2 r.5 `A-le-lu-ja,` vs C v1 r.6 `Aleluja,`; A v2 r.5 `ti.` vs C v1 r.6 `ti`
     - veľkosť písmen: A v1 r.1 `ty` vs C v1 r.1 `Ty`; A v1 r.1 `Skalou,` vs C v1 r.1 `skalou,`; A v1 r.2 `ty` vs C v1 r.1 `Ty`; A v1 r.3 `teba` vs C v1 r.2 `Teba`; A v2 r.1 `ty` vs C v1 r.4 `Ty`; A v2 r.3 `ty` vs C v1 r.5 `Ty`; A v2 r.4 `ti.` vs C v1 r.5 `Ti.`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v C: `R:`×2

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Prijímanie` · tituly: – · text: nič unikátne
- **B**: tagy: `Anonymous` · tituly: – · text: nič unikátne
- **C**: tagy: `detsky zbor` · tituly: `Jezis ty si skalou` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.3: `R:`; v1 r.6: `R:`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Ježiš, ty si skalou (Prijímanie).xml` (A)
- **Zmazať / zlúčiť:** `Ježiš, ty si skalou (Anonymous).xml` (B), `Jezis ty si skalou (detsky zbor).xml` (C) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A a B majú rovnaké slová (rozdiel 0); líšia sa zápisom opakovania: A `|: … :|` pre blok 4 riadkov, B `/: … :/` pri každom riadku osobitne a prázdny riadok na konci v2.
  - C má dve slohy v jednej sloha `v1` s číslami `1.` a `2.` v texte a pokynmi `R: Aleluja, mojím štítom si.` / `R: Aleluja, dôverujem ti` – pokyny sa zobrazia na slajde.
  - A má reálny tag `Prijímanie`, B zástupný `Anonymous`, C `detsky zbor`.
  - Písanie „aleluja“ je nejednotné: A `A-le-lu-ja, mojím štítom si.`, B `Aleluja, dôverujem ti.` (v2) a `A-le-lu-ja mojím štítom si.` (v1), C `Aleluja`.
- **Čo prevziať z ostatných:**
  - Pridať tag `detsky zbor`.
  - Voliteľne zjednotiť `A-le-lu-ja`/`Aleluja`.
- **Istota:** vysoká – Obsah je totožný, ostatné súbory len pridávajú pokyny alebo iný zápis.

**Riziká a neistoty:**

- Pomlčky v `A-le-lu-ja` môžu byť zámerné (delenie slabík).

---

<a id="g22"></a>
## G22 · [4c] `Kríž je znakom spásy (Pôstna, krížová cesta).xml` · `Kríž je znakom spásy (Anonymous).xml` · `Kriz je znakom spasy (detsky zbor).xml`

**Zhrnutie:** Rovnaký text; A má najúplnejšie poradie hrania a správnu interpunkciu, ale pokyn `R:` a nezlomiteľné medzery; B nemá `verseOrder`, C má na konci `c1` dvakrát.

Existuje aj verzia s akordmi: `Kriz je znakom spasy (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Kríž je znakom spásy (Pôstna, krížová cesta).xml`
- **B** = `Kríž je znakom spásy (Anonymous).xml`
- **C** = `Kriz je znakom spasy (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B | C |
|---|---|---|---|
| Zodpovedá konvencii názvu | áno | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | áno / áno | nie / nie | nie / nie |
| Tituly | `Kríž je znakom spásy` | `Kríž je znakom spásy` | `Kriz je znakom spasy` |
| Tagy (`<author>`) | `krížová cesta`, `Pôstna` | `Anonymous` | `detsky zbor` |
| songbooks | – | – | – |
| verseOrder | `v1 v2 v1 v3 v1 v4 v1` | – | `c1 v1 c1 v2 c1 v3 c1 c1` |
| copyright / ccliNo | – / – | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4` | `c1 v1 v2 v3` | `v1 v2 v3 c1` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 4 / 4 | 4 / 4 |
| Počet riadkov (neprázdnych) | 12 (12) | 8 (8) | 14 (14) |
| Počet slov (bez čísel slôh) | 62 | 61 | 61 |
| verseOrder vs dokument | líši sa od poradia v dokumente | – | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 110 | 61 | 121 |
| Riadky s číslom slohy na začiatku (`1.`) | 3 | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF | CRLF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- A v1 r.1: `R: Kríž je znakom spásy,`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 62 slov v A, 61 slov v B; 1 miest s rozdielom obsahu
1. [pokyn v texte] A v1 r.1: `R:` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 6
     - interpunkcia: A v1 r.2 `kríž,` vs B c1 r.1 `kríž`; A v2 r.1 `si,` vs B v1 r.1 `si`; A v2 r.1 `Pane,` vs B v1 r.1 `Pane`; A v2 r.1 `znášal` vs B v1 r.1 `znášal,`; A v3 r.1 `hľa,` vs B v2 r.1 `hľa`; A v4 r.2 `vín,` vs B v3 r.1 `vín.`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `R:`×1; viac v B: –
   - V poradí hrania (po rozbalení verseOrder): 110 vs 61 slov, 4 miest s rozdielom obsahu: A `R:` vs B ``; A `R: Kríž je znakom spásy, kríž, ten drevený, … (16 slov)` vs B ``; A `R: Kríž je znakom spásy, kríž, ten drevený, … (16 slov)` vs B ``; A `R: Kríž je znakom spásy, kríž, ten drevený, … (16 slov)` vs B ``

*Dvojica A ↔ C:* 62 slov v A, 61 slov v C; 1 miest s rozdielom obsahu
2. [rovnaký text na inom mieste (iné poradie slôh)] A v1 r.1–4 a C c1 r.1–2: `R: Kríž je znakom spásy, kríž, ten drevený, Kristom nesený … (16 slov)`
     - v presunutom úseku: A `R:` vs C ``
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 4, veľkosť písmen: 1
     - interpunkcia: A v2 r.1 `si,` vs C v1 r.1 `si`; A v2 r.1 `Pane,` vs C v1 r.1 `Pane`; A v3 r.1 `hľa,` vs C v2 r.1 `hľa`; A v4 r.2 `vín,` vs C v3 r.2 `vín.`
     - veľkosť písmen: A v4 r.4 `ním.` vs C v3 r.4 `Ním.`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `R:`×1; viac v C: –
   - V poradí hrania (po rozbalení verseOrder): 110 vs 121 slov, 5 miest s rozdielom obsahu: A `R:` vs C ``; A `R:` vs C ``; A `R:` vs C ``; A `R:` vs C ``; A `` vs C `Kríž je znakom spásy, kríž ten drevený, Kristom … (15 slov)`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Pôstna`, `krížová cesta` · tituly: `Kríž je znakom spásy` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1: `R:`
- **B**: tagy: `Anonymous` · tituly: `Kríž je znakom spásy` · text: nič unikátne
- **C**: tagy: `detsky zbor` · tituly: `Kriz je znakom spasy` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1–2: `Kríž je znakom spásy, kríž ten drevený, Kristom nesený z lásky, krvou zmáčaný za nás.`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Kríž je znakom spásy (Pôstna, krížová cesta).xml` (A)
- **Zmazať / zlúčiť:** `Kríž je znakom spásy (Anonymous).xml` (B), `Kriz je znakom spasy (detsky zbor).xml` (C) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Slovo po slove sú súbory totožné; jediný rozdiel je pokyn `R:` v A (v1 r.1: `R: Kríž je znakom spásy,`).
  - A hrá `v1 v2 v1 v3 v1 v4 v1` (refrén na začiatku, medzi slohami aj na konci); B nemá `verseOrder`, takže refrén zaznie raz na začiatku (61 slov oproti 110 po rozbalení v A); C hrá `c1 v1 c1 v2 c1 v3 c1 c1`, teda refrén na konci dvakrát.
  - Interpunkcia: A `Sám si, Pane, znášal ťarchu našich vín.`, B `Sám si Pane znášal, ťarchu našich vín.` (čiarka na nesprávnom mieste), C `Sám si Pane znášal ťarchu našich vín.` (bez čiarok).
  - A má v titule aj v názve súboru nezlomiteľné medzery; C má titul bez diakritiky `Kriz je znakom spasy`; C delí na krátke riadky (4 na slohu).
- **Čo prevziať z ostatných:**
  - V A odstrániť pokyn `R:` a nahradiť nezlomiteľné medzery v titule/názve bežnými; pridať tag `detsky zbor`.
- **Istota:** stredná – Text je rovnaký; voľba A vychádza z poradia hrania a interpunkcie, C má čistejšie delenie riadkov.

**Riziká a neistoty:**

- Duplicitné `c1 c1` na konci C môže byť zámerné (opakovanie refrénu na záver).

---

<a id="g23"></a>
## G23 · [4c] `Môj Boh, vďaka tebe dýcham (Prijímanie).xml` · `moj boh (detsky zbor).xml`

**Zhrnutie:** A obsahuje všetko z B plus riadok navyše, ale má preklep `zmelina`.

**Súbory v skupine:**
- **A** = `Môj Boh, vďaka tebe dýcham (Prijímanie).xml`
- **B** = `moj boh (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Môj Boh, vďaka tebe dýcham` | `moj boh` |
| Tagy (`<author>`) | `Prijímanie` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3` | `v1a v1b` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 2 / 2 |
| Počet riadkov (neprázdnych) | 11 (11) | 17 (12) |
| Počet slov (bez čísel slôh) | 57 | 52 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 57 | 52 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 5 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 57 slov v A, 52 slov v B; 2 miest s rozdielom obsahu
1. [preklep / zmena slova] A v2 r.4: `zmelina`  vs  B v1b r.5: `zmenila`
     - riadok v A: `zmelina môj svet.`
     - riadok v B: `zmenila môj svet.`
2. [chýba v B] A v3 r.2: `ona zmení aj tvoj svet.` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 4, veľkosť písmen: 1
     - interpunkcia: A v1 r.2 `som` vs B v1a r.2 `som.`; A v2 r.2 `je,` vs B v1b r.3 `je`; A v2 r.3 `je,` vs B v1b r.4 `je`; A v3 r.1 `svet,` vs B v1b r.7 `svet.`
     - veľkosť písmen: A v1 r.3 `a` vs B v1a r.3 `A`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `aj`×1, `ona`×1, `svet.`×1, `tvoj`×1, `zmelina`×1, `zmení`×1; viac v B: `zmenila`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Prijímanie` · tituly: `Môj Boh, vďaka tebe dýcham` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.4: `zmelina`; v3 r.2: `ona zmení aj tvoj svet.`
- **B**: tagy: `detsky zbor` · tituly: `moj boh` · text (slová, ktoré v žiadnom inom súbore nie sú): v1b r.5: `zmenila`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Môj Boh, vďaka tebe dýcham (Prijímanie).xml` (A)
- **Zmazať / zlúčiť:** `moj boh (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A má v3 `Ona zmenila môj svet,` / `ona zmení aj tvoj svet.`; B končí iba `Ona zmenila môj svet.` – chýba jej riadok `ona zmení aj tvoj svet.`
  - A má preklep `zmelina môj svet.` (v2 r.4); B má správne `zmenila môj svet.`
  - B má 5 prázdnych riadkov (`<br/><br/>`) vo `v1a`/`v1b` a titul bez diakritiky `moj boh`; A má 0 prázdnych riadkov.
  - B nemá žiadny unikátny text ani tag okrem `detsky zbor`.
- **Čo prevziať z ostatných:**
  - V A opraviť `zmelina` → `zmenila`; pridať tag `detsky zbor`.
- **Istota:** vysoká – A je nadmnožina B, rozdiel je jediný preklep.

**Riziká a neistoty:**

- Posledný riadok `ona zmení aj tvoj svet.` nie je overený žiadnym iným zdrojom.

---

<a id="g24"></a>
## G24 · [4c] `Taky Velky Taky maly (detsky zbor).xml` · `Môžeš svätým byť (Večeradlo s Pannou Máriou).xml`

**Zhrnutie:** B nemá riadok `Aj plešatý aj vlasatý môžeš svätým byť.` a namiesto neho má dvakrát `Ako ja, tak aj ty môžeš svätým byť.`

Existuje aj verzia s akordmi: `Taky Velky Taky maly (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Taky Velky Taky maly (detsky zbor).xml`
- **B** = `Môžeš svätým byť (Večeradlo s Pannou Máriou).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Taky Velky Taky maly` | `Môžeš svätým byť` |
| Tagy (`<author>`) | `detsky zbor` | `Večeradlo s Pannou Máriou` |
| songbooks | – | – |
| verseOrder | `c1 v1 c1 v2 c1 v3` | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 c1` | `c1 v1 v2 v3` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 4 / 4 |
| Počet riadkov (neprázdnych) | 10 (10) | 18 (18) |
| Počet slov (bez čísel slôh) | 64 | 65 |
| verseOrder vs dokument | líši sa od poradia v dokumente | – |
| Slov po rozbalení verseOrder | 122 | 65 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 64 slov v A, 65 slov v B; 1 miest s rozdielom obsahu
1. [rovnaký text na inom mieste (iné poradie slôh)] A c1 r.1–4 a B c1 r.1–6: `Taký veľký, taký malý, môže svätým byť. Taký tučný, taký … (29 slov)`
     - v presunutom úseku: A `` vs B `Ako ja, tak`
     - v presunutom úseku: A `plešatý aj vlasatý` vs B `ty`
   - Žiadne rozdiely v zápise (diakritika / veľkosť / interpunkcia) pri zhodných slovách.
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `Aj`×1, `plešatý`×1, `vlasatý`×1; viac v B: `Ako`×1, `ja,`×1, `tak`×1, `ty`×1
   - V poradí hrania (po rozbalení verseOrder): 122 vs 65 slov, 4 miest s rozdielom obsahu: A `` vs B `Ako ja, tak`; A `plešatý aj vlasatý` vs B `ty`; A `Taký veľký, taký malý, môže svätým byť. Taký … (29 slov)` vs B ``; A `Taký veľký, taký malý, môže svätým byť. Taký … (29 slov)` vs B ``

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `detsky zbor` · tituly: `Taky Velky Taky maly` · verseOrder `c1 v1 c1 v2 c1 v3` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1–4: `Taký veľký, taký malý, môže svätým byť. Taký tučný, taký chudý môže svätým byť. Aj plešatý … (29 slov)`
- **B**: tagy: `Večeradlo s Pannou Máriou` · tituly: `Môžeš svätým byť` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1–6: `Taký veľký, taký malý, môže svätým byť. Taký tučný, taký chudý môže svätým byť. Ako ja, … (30 slov)`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Taky Velky Taky maly (detsky zbor).xml` (A)
- **Zmazať / zlúčiť:** `Môžeš svätým byť (Večeradlo s Pannou Máriou).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A má refrén v 4 riadkoch vrátane `Aj plešatý aj vlasatý môžeš svätým byť.`; B má refrén v 6 riadkoch, v ktorých riadok o plešatých chýba a `Ako ja, tak aj ty môžeš svätým byť.` stojí dvakrát (c1 r.5–6).
  - A má `verseOrder` `c1 v1 c1 v2 c1 v3`; B nemá `verseOrder` (refrén je v B prvá sloha, zaznie raz).
  - B má správny titul `Môžeš svätým byť` a tag `Večeradlo s Pannou Máriou`; A má titul `Taky Velky Taky maly` bez diakritiky.
  - Slohy v1–v3 majú v oboch rovnaký text (len iné delenie riadkov).
- **Čo prevziať z ostatných:**
  - Titul A opraviť na «Taký veľký, taký malý» a pridať druhý titul `Môžeš svätým byť`; pridať tag `Večeradlo s Pannou Máriou`.
- **Istota:** stredná – Úplnejší refrén je v A, ale nie je overené, ktorý variant je pôvodný.

**Riziká a neistoty:**

- Možno B zámerne zdvojuje riadok `Ako ja, tak aj ty` (zbor spieva dvakrát).

---

<a id="g25"></a>
## G25 · [4c] `Nebojim sa (Author Unknown).xml` · `Nebojim sa (detsky zbor).xml`

**Zhrnutie:** Obsah je rovnaký až na jeden preklep v B (`potrebujeme,`), ktorý sa dá opraviť podľa A.

**Súbory v skupine:**
- **A** = `Nebojim sa (Author Unknown).xml`
- **B** = `Nebojim sa (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Nebojim sa` | `Nebojim sa` |
| Tagy (`<author>`) | `Author Unknown` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | `c1 v1 c1 v2 c1` | `c1 v1 c1 v2 c1` |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 c1` | `v1 v2 c1` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 3 / 3 |
| Počet riadkov (neprázdnych) | 5 (5) | 5 (5) |
| Počet slov (bez čísel slôh) | 66 | 65 |
| verseOrder vs dokument | líši sa od poradia v dokumente | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 90 | 89 |
| Riadky s číslom slohy na začiatku (`1.`) | 2 | 2 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 2 | 2 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica B ↔ A:* 65 slov v B, 66 slov v A; 1 miest s rozdielom obsahu
1. [preklep / zmena slova] B v1 r.2: `potrebujeme,`  vs  A v1 r.2: `potrebujem ťa,`
     - riadok v B: `nosíš. Vďaka Ti Otec a viem to isto, keď potrebujeme, vždy si mi blízko!`
     - riadok v A: `nosíš. Vďaka Ti Otec a viem to isto, keď potrebujem ťa, vždy si mi blízko!`
   - Žiadne rozdiely v zápise (diakritika / veľkosť / interpunkcia) pri zhodných slovách.
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v B: `potrebujeme,`×1; viac v A: `potrebujem.`×1, `Ťa`×1
   - V poradí hrania (po rozbalení verseOrder): 89 vs 90 slov, 1 miest s rozdielom obsahu: B `potrebujeme,` vs A `potrebujem ťa,`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Author Unknown` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.2: `potrebujem ťa,`
- **B**: tagy: `detsky zbor` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.2: `potrebujeme,`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Nebojim sa (detsky zbor).xml` (B)
- **Zmazať / zlúčiť:** `Nebojim sa (Author Unknown).xml` (A) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Jediný rozdiel: A `keď potrebujem ťa, vždy si mi blízko!` (v1 r.2) vs B `keď potrebujeme, vždy si mi blízko!` – v B zlá osoba slovesa.
  - Štruktúra je identická: `verseOrder` `c1 v1 c1 v2 c1`, slohy `1.`/`2.` a `c1`.
  - B má reálny tag `detsky zbor` (A len zástupný `Author Unknown`), takže po oprave jedného slova sa názov súboru B nemení.
  - Titul je v oboch bez diakritiky (`Nebojim sa`), v texte je `Nebojím sa aj keď je tma`.
- **Čo prevziať z ostatných:**
  - V B nahradiť `keď potrebujeme,` → `keď potrebujem ťa,`; titul opraviť na «Nebojím sa».
- **Istota:** vysoká – Rozdiel je jediné slovo a správnu podobu ukazuje A aj logika vety.

**Riziká a neistoty:**

- Premenovanie súboru pri oprave titulu na «Nebojím sa (detsky zbor).xml».

---

<a id="g26"></a>
## G26 · [4c] `Nech vás požehnáva Pán (Author Unknown).xml` · `nech vas pozehnava pan (detsky zbor).xml` · `Požehnanie sv.Františka (Jerichove Trúby, svadobná).xml`

**Zhrnutie:** Rovnaký text, ale iba A má záver napísaný ako text; C obsahuje pokyny a preklep `váš`, B záver nemá.

**Súbory v skupine:**
- **A** = `Nech vás požehnáva Pán (Author Unknown).xml`
- **B** = `nech vas pozehnava pan (detsky zbor).xml`
- **C** = `Požehnanie sv.Františka (Jerichove Trúby, svadobná).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B | C |
|---|---|---|---|
| Zodpovedá konvencii názvu | áno | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie | nie / nie |
| Tituly | `Nech vás požehnáva Pán` | `nech vas pozehnava pan` | `Požehnanie sv.Františka` |
| Tagy (`<author>`) | `Author Unknown` | `detsky zbor` | `Jerichove Trúby`, `svadobná` |
| songbooks | – | – | – |
| verseOrder | – | – | – |
| copyright / ccliNo | – / – | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2` | `v1` | `v1 v2 v3` |
| Počet slôh / `<lines>` blokov | 2 / 2 | 1 / 1 | 3 / 3 |
| Počet riadkov (neprázdnych) | 12 (11) | 4 (4) | 9 (9) |
| Počet slov (bez čísel slôh) | 52 | 40 | 49 |
| verseOrder vs dokument | – | – | – |
| Slov po rozbalení verseOrder | 52 | 40 | 49 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 | 2 |
| Prázdne riadky (`<br/><br/>`) | 1 | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- C v2 r.4: `Nech vás požehnáva Pán			celé 3x`
- C v2 r.4: `Nech vás požehnáva Pán			celé 3x`
- C v3 r.1: `+ na záver      Nech vás požehnáva Pán   3x`
- C v3 r.1: `+ na záver      Nech vás požehnáva Pán   3x`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 52 slov v A, 40 slov v B; 1 miest s rozdielom obsahu
1. [chýba v B] A v2 r.1–3: `...nech Vás požehnáva Pán, nech Vás požehnáva Pán, nech Vás požehnáva Pán.` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 9, interpunkcia: 2
     - veľkosť písmen: A v1 r.1 `Vás` vs B v1 r.1 `vás`; A v1 r.2 `Vás` vs B v1 r.1 `vás`; A v1 r.3 `nech` vs B v1 r.2 `Nech`; A v1 r.3 `Vám` vs B v1 r.2 `vám`; A v1 r.4 `Vám` vs B v1 r.2 `vám.`; A v1 r.6 `Vám` vs B v1 r.3 `vám`; A v1 r.7 `Vám` vs B v1 r.3 `vám`; A v1 r.8 `a` vs B v1 r.4 `A` … (+1)
     - interpunkcia: A v1 r.2 `Pán,` vs B v1 r.1 `Pán.`; A v1 r.7 `dá` vs B v1 r.3 `dá.`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `Nech`×3, `Pán,`×3, `požehnáva`×3, `Vás`×3; viac v B: –

*Dvojica A ↔ C:* 52 slov v A, 49 slov v C; 3 miest s rozdielom obsahu
2. [iný text] A v1 r.3: `tvár`  vs  C v1 r.3: `tvá-ááááá-ár`
     - riadok v A: `nech Vám ukáže svoju tvár`
     - riadok v C: `Nech vám ukáže svoju tvá-ááááá-ár`
3. [chýba v A] C v2 r.4 – v3 r.1: `celé 3x na záver` – v A tento text nie je
4. [iný text] A v2 r.2–3: `nech Vás požehnáva Pán, nech Vás požehnáva Pán.`  vs  C v3 r.1: `3x`
   - Rozdiely len v zápise (rovnaké slová): diakritika + veľkosť písmen: 1, interpunkcia: 5, veľkosť písmen: 14
     - diakritika + veľkosť písmen: A v1 r.1 `Vás` vs C v1 r.1 `váš`
     - interpunkcia: A v1 r.1 `Pán,` vs C v1 r.1 `Pán`; A v1 r.2 `Pán,` vs C v1 r.2 `Pán`; A v1 r.8 `raz,` vs C v2 r.3 `raz`; A v1 r.9 `Pán.` vs C v2 r.4 `Pán`; A v2 r.1 `Pán,` vs C v3 r.1 `Pán`
     - veľkosť písmen: A v1 r.2 `nech` vs C v1 r.2 `Nech`; A v1 r.2 `Vás` vs C v1 r.2 `vás`; A v1 r.3 `nech` vs C v1 r.3 `Nech`; A v1 r.3 `Vám` vs C v1 r.3 `vám`; A v1 r.4 `a` vs C v1 r.4 `A`; A v1 r.4 `Vám` vs C v1 r.4 `vám`; A v1 r.6 `Vám` vs C v2 r.1 `vám`; A v1 r.7 `a` vs C v2 r.2 `A` … (+6)
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `Nech`×2, `Pán,`×2, `požehnáva`×2, `tvár`×1, `Vás`×2; viac v C: `3x`×2, `celé`×1, `na`×1, `tvá-ááááá-ár`×1, `záver`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Author Unknown` · tituly: `Nech vás požehnáva Pán` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.2–3: `nech Vás požehnáva Pán, nech Vás požehnáva Pán.`
- **B**: tagy: `detsky zbor` · tituly: `nech vas pozehnava pan` · text: nič unikátne
- **C**: tagy: `Jerichove Trúby`, `svadobná` · tituly: `Požehnanie sv.Františka` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.3: `tvá-ááááá-ár`; v2 r.4 – v3 r.1: `celé 3x na záver`; v3 r.1: `3x`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Nech vás požehnáva Pán (Author Unknown).xml` (A)
- **Zmazať / zlúčiť:** `nech vas pozehnava pan (detsky zbor).xml` (B), `Požehnanie sv.Františka (Jerichove Trúby, svadobná).xml` (C) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A má záver `...nech Vás požehnáva Pán,` 3× v `v2` (12 slov navyše); B (40 slov) ho nemá a C ho má iba ako pokyn `+ na záver      Nech vás požehnáva Pán   3x` (v3 r.1).
  - C má v texte pokyny a tabulátory: `Nech vás požehnáva Pán			celé 3x` (v2 r.4), natiahnuté `tvá-ááááá-ár` (v1 r.3) a preklep `Nech váš požehnáva Pán` (v1 r.1).
  - A má jeden prázdny riadok v `v1` a veľké `Vás`/`Vám`; B píše `vás`/`vám` malým.
  - Tagy: C má reálne `Jerichove Trúby`, `svadobná`; B `detsky zbor`; A len zástupný `Author Unknown`.
- **Čo prevziať z ostatných:**
  - Pridať tagy `Jerichove Trúby`, `svadobná`, `detsky zbor` (zástupný `Author Unknown` vynechať) → názov «Nech vás požehnáva Pán (Jerichove Trúby, detsky zbor, svadobná).xml».
  - Pridať druhý titul «Požehnanie sv. Františka» (z C).
- **Istota:** stredná – Obsah A je úplný, ale pokyn „celé 3x“ (opakovať celé) sa textom nedá preniesť.

**Riziká a neistoty:**

- Pokyn `celé 3x` z C sa stratí; ak je potrebný, riešiť `verseOrder`.

---

<a id="g27"></a>
## G27 · [4c] `NEPOŠKVRNENÉ SRDCE MÁRIE (Mariánska, Veceradlo).xml` · `Neposkvrnene Srdce Marie (detsky zbor).xml`

**Zhrnutie:** Rovnaký obsah; A zapisuje opakovania značkami `[: :]` a pokynom `(3x)`, B ich vypisuje a zároveň označuje `/: :/`.

**Súbory v skupine:**
- **A** = `NEPOŠKVRNENÉ SRDCE MÁRIE (Mariánska, Veceradlo).xml`
- **B** = `Neposkvrnene Srdce Marie (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `NEPOŠKVRNENÉ SRDCE MÁRIE` | `Neposkvrnene Srdce Marie` |
| Tagy (`<author>`) | `Mariánska`, `Veceradlo` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4` | `v1 v2 v3 v4` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 4 / 4 |
| Počet riadkov (neprázdnych) | 13 (13) | 20 (20) |
| Počet slov (bez čísel slôh) | 53 | 82 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 53 | 82 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 12 | 8 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- A v1 r.2: `si svetlom a cestou (3x)`
- A v1 r.2 (zátvorka): `(3x)`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 53 slov v A, 82 slov v B; 6 miest s rozdielom obsahu
1. [chýba v A (opakovanie vypísané v B)] B v1 r.1: `Nepoškvrnené Srdce Márie,` – v A tento text nie je
2. [iný text] A v1 r.2: `(3x)`  vs  B v1 r.4–5: `si svetlom a cestou, si svetlom a cestou`
3. [chýba v A] B v2 r.2–3: `zasvätení kňazi Tebe, Mária, dávajú sa s láskou,` – v A tento text nie je
4. [chýba v A (opakovanie vypísané v B)] B v3 r.4: `nech skoro zvíťazí` – v A tento text nie je
5. [chýba v A (opakovanie vypísané v B)] B v4 r.1: `Keď príde posledná hodina naša,` – v A tento text nie je
6. [chýba v A (opakovanie vypísané v B)] B v4 r.4–5: `nemeškaj, príď, Matka` – v A tento text nie je
   - Rozdiely len v zápise (rovnaké slová): značky opakovania: 14, interpunkcia: 2, veľkosť písmen: 1
     - značky opakovania: A v1 r.1 `[:Nepoškvrnené` vs B v1 r.2 `Nepoškvrnené`; A v1 r.1 `Márie:],` vs B v1 r.2 `Márie,`; A v1 r.3 `zemi.` vs B v1 r.5 `zemi.:/`; A v2 r.1 `[:Zasvätení` vs B v2 r.1 `Zasvätení`; A v2 r.1 `Mária,:]` vs B v2 r.1 `Mária,`; A v2 r.2 `[:dávajú` vs B v2 r.4 `dávajú`; A v2 r.2 `láskou,:]` vs B v2 r.4 `láskou,`; A v2 r.3 `Kristovi.` vs B v2 r.5 `Kristovi.:/` … (+6)
     - interpunkcia: A v1 r.2 `cestou` vs B v1 r.3 `cestou,`; A v3 r.3 `zvíťazí:]` vs B v3 r.3 `zvíťazí,`
     - veľkosť písmen: A v4 r.1 `[:Keď` vs B v4 r.2 `keď`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `(3x)`×1; viac v B: `a`×2, `cestou`×2, `[:dávajú`×1, `hodina`×1, `[:Keď`×1, `kňazi`×1, `láskou,:]`×1, `Mária,:]`×1, `Márie:],`×1, `Matka,`×1, `naša,:]`×1, `[:nech`×1, `nemeškaj,:]`×1, `[:Nepoškvrnené`×1, `posledná`×1, `[:príď,`×1, `príde`×1, `s`×1, `sa`×1, `si`×2, `skoro`×1, `Srdce`×1, `svetlom`×2, `Tebe,`×1, `[:Zasvätení`×1, `zvíťazí:]`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Mariánska`, `Veceradlo` · tituly: `NEPOŠKVRNENÉ SRDCE MÁRIE` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.2: `(3x)`
- **B**: tagy: `detsky zbor` · tituly: `Neposkvrnene Srdce Marie` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1: `Nepoškvrnené Srdce Márie,`; v1 r.4–5: `si svetlom a cestou, si svetlom a cestou`; v2 r.2–3: `zasvätení kňazi Tebe, Mária, dávajú sa s láskou,`; v3 r.4: `nech skoro zvíťazí`; v4 r.1: `Keď príde posledná hodina naša,`; v4 r.4–5: `nemeškaj, príď, Matka`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `NEPOŠKVRNENÉ SRDCE MÁRIE (Mariánska, Veceradlo).xml` (A)
- **Zmazať / zlúčiť:** `Neposkvrnene Srdce Marie (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B vypisuje opakovania (`Nepoškvrnené Srdce Márie,` 2× v v1 r.1–2, `zasvätení kňazi Tebe, Mária,` 2× v v2 r.1–2), A ich zapisuje `[:Nepoškvrnené Srdce Márie:],`.
  - B navyše okolo vypísaných riadkov dáva `/: si svetlom a cestou,` … `si svetlom a cestou nám na zemi.:/`, takže pri spievaní podľa značiek by sa opakovali dvakrát; A je kompaktnejšia (13 riadkov oproti 20).
  - A obsahuje pokyn `(3x)` v texte (v1 r.2: `si svetlom a cestou (3x)`), ktorý sa zobrazí na slajde.
  - A má tagy `Mariánska`, `Veceradlo` (bez diakritiky, inde `Večeradlo s Pannou Máriou`); B `detsky zbor`; titul B bez diakritiky `Neposkvrnene Srdce Marie`.
- **Čo prevziať z ostatných:**
  - Pridať tag `detsky zbor`; voliteľne opraviť tag `Veceradlo`.
- **Istota:** stredná – Nie je jasné, či detský zbor potrebuje vypísané opakovania.

**Riziká a neistoty:**

- Ak sa B zmaže, stratí sa vypísaná (neopakujúca sa) podoba, ktorá zobrazí každý riadok samostatne.

---

<a id="g28"></a>
## G28 · [4c] `Nežne zlomený (...).xml` · `Ku krížu dvíham zrak - Nežne zlomený (Rieka Života).xml`

**Zhrnutie:** B obsahuje tú istú slohu dvakrát (v2 = v3); inak je obsah rovnaký.

**Súbory v skupine:**
- **A** = `Nežne zlomený (...).xml`
- **B** = `Ku krížu dvíham zrak - Nežne zlomený (Rieka Života).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Nežne zlomený` | `Ku krížu dvíham zrak - Nežne zlomený` |
| Tagy (`<author>`) | `...` | `Rieka Života` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1a v1b c1 v2a v2b v3` | `v1 c1 v2 v3 e1` |
| Počet slôh / `<lines>` blokov | 6 / 6 | 5 / 5 |
| Počet riadkov (neprázdnych) | 23 (23) | 19 (19) |
| Počet slov (bez čísel slôh) | 98 | 128 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 98 | 128 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 3 | 5 |
| Riadky s dvojitou medzerou vnútri | 0 | 2 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- A c1 r.4 (zátvorka): `(ma)`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 98 slov v A, 128 slov v B; 2 miest s rozdielom obsahu
1. [preklep / zmena slova] A v1a r.1–2: `zrak ku`  vs  B v1 r.1: `zrak,ku`
     - riadok v A: `Ku krížu dvíham zrak`
     - riadok v B: `Ku krížu dvíham zrak,ku krížu viniem sa`
2. [iný text] A v2b r.3: `viacej`  vs  B v2 r.4 – v3 r.4: `viac už Tvoj hnev Ježišov kríž zmieril ma Aký vzácny dar, život, ktorý mám … (32 slov)`
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 8, interpunkcia: 6
     - veľkosť písmen: A v1a r.3 `pijem` vs B v1 r.2 `Pijem`; A v1b r.3 `v` vs B v1 r.4 `V`; A v1b r.3 `ňom` vs B v1 r.4 `Ňom`; A v1b r.4 `Spravodlivý` vs B v1 r.4 `spravodlivý`; A c1 r.2 `viac` vs B c1 r.2 `Viac`; A c1 r.4 `v` vs B c1 r.3 `V`; A v2a r.3 `ten,` vs B v2 r.2 `Ten,`; A v2b r.3 `nie` vs B v2 r.4 `Nie`
     - interpunkcia: A v1a r.3 `rán` vs B v1 r.2 `rán,`; A v1b r.1 `môj` vs B v1 r.3 `môj,`; A c1 r.1 `ma` vs B c1 r.1 `ma,`; A c1 r.2 `kolená,` vs B c1 r.1 `kolená`; A c1 r.4 `(ma)` vs B c1 r.3 `ma.`; A v2a r.1 `dar` vs B v2 r.1 `dar,`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `Ku`×1, `viacej`×1, `zrak`×1; viac v B: `Aký`×1, `čo`×1, `dar`×1, `daroval`×1, `hnev`×1, `je`×1, `Ježišov`×1, `k`×1, `Kristus`×1, `kríž`×2, `ktorý`×1, `ma`×2, `mám`×1, `mi`×1, `nie`×1, `povolal`×1, `sám`×1, `si`×1, `skrze`×1, `smrti`×1, `ten,`×1, `Tvoj`×1, `už`×1, `viac`×2, `vzácny`×1, `život,`×1, `životu`×1, `zmieril`×1, `Zo`×1, `zrak,ku`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `...` · tituly: `Nežne zlomený` · text (slová, ktoré v žiadnom inom súbore nie sú): v1a r.1–2: `zrak ku`; v2b r.3: `viacej`
- **B**: tagy: `Rieka Života` · tituly: `Ku krížu dvíham zrak - Nežne zlomený` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1: `zrak,ku`; v2 r.4 – v3 r.4: `viac už Tvoj hnev Ježišov kríž zmieril ma Aký vzácny dar, život, ktorý mám Ten, čo … (32 slov)`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Nežne zlomený (...).xml` (A)
- **Zmazať / zlúčiť:** `Ku krížu dvíham zrak - Nežne zlomený (Rieka Života).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - V B sú slohy `v2` a `v3` slovo po slove rovnaké (5 riadkov `Aký vzácny dar, život, ktorý mám` … `Ježišov kríž zmieril ma`); A ju má raz (`v2a` + `v2b`), takže B má o 30 slov viac (128 vs 98).
  - B má zlepené slová `zrak,ku krížu viniem sa` (v1 r.1) a koncovku `e1`, ktorá je v A ako `v3` (rovnaké slová `V úžase z kríža vyznať chcem`).
  - Slovný rozdiel: A `nie je viacej už Tvoj hnev` (v2b r.3) vs B `Nie je viac už Tvoj hnev`.
  - B má reálny tag `Rieka Života` a dlhší titul `Ku krížu dvíham zrak - Nežne zlomený`; A má zástupný tag `...`.
- **Čo prevziať z ostatných:**
  - Pridať tag `Rieka Života` a druhý titul `Ku krížu dvíham zrak - Nežne zlomený`; voliteľne `viacej` → `viac`.
- **Istota:** vysoká – B je A + zdvojená sloha; nič unikátne.

**Riziká a neistoty:**

- Ak je zdvojenie v2 = v3 zámerné (sloha sa spieva dvakrát), treba to riešiť cez `verseOrder` v A.

---

<a id="g29"></a>
## G29 · [4c] `Ty mi dávaš nohy jeleníc (Anonymous).xml` · `Nohy jeleníc (Prijímanie).xml`

**Zhrnutie:** Rovnaký text až na jedno slovo (`duši` vs `ceste`); A delí text na slajdy, B ho má v jednej 8-riadkovej sloha.

**Súbory v skupine:**
- **A** = `Ty mi dávaš nohy jeleníc (Anonymous).xml`
- **B** = `Nohy jeleníc (Prijímanie).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Ty mi dávaš nohy jeleníc` | `Nohy jeleníc` |
| Tagy (`<author>`) | `Anonymous` | `Prijímanie` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 c1 c2` | `v1` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 1 / 1 |
| Počet riadkov (neprázdnych) | 12 (12) | 8 (7) |
| Počet slov (bez čísel slôh) | 48 | 48 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 48 | 48 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 1 |
| Riadky s koncovou medzerou | 1 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 48 slov v A, 48 slov v B; 1 miest s rozdielom obsahu
1. [iný text] A v1 r.4: `duši`  vs  B v1 r.4: `ceste`
     - riadok v A: `a mojej duši dáš pečať víťazstva.`
     - riadok v B: `a mojej ceste dáš pečať víťazstva.`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 1, veľkosť písmen: 1
     - interpunkcia: A c1 r.4 `položíš.` vs B v1 r.7 `položíš,`
     - veľkosť písmen: A c2 r.1 `Nikto` vs B v1 r.8 `nikto`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `duši`×1; viac v B: `ceste`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Anonymous` · tituly: `Ty mi dávaš nohy jeleníc` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.4: `duši`
- **B**: tagy: `Prijímanie` · tituly: `Nohy jeleníc` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.4: `ceste`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Ty mi dávaš nohy jeleníc (Anonymous).xml` (A)
- **Zmazať / zlúčiť:** `Nohy jeleníc (Prijímanie).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Jediný slovný rozdiel: `a mojej duši dáš pečať víťazstva.` (A, v1 r.4) vs `a mojej ceste dáš pečať víťazstva.` (B, v1 r.4).
  - A delí text na tri slohy po 4 riadkoch (`v1`, `c1`, `c2`), B má jednu sloha s prázdnym riadkom a posledný riadok je dlhý (14 slov): `nikto už nevezme, čo si mi zasľúbil, so žalmom na perách zaspávam v pokoji.`
  - A označuje 2. a 3. štvorveršie ako `c1`/`c2` (refrén), hoci ide o textové slohy – pomenovanie je zavádzajúce.
  - Tagy: A zástupný `Anonymous`, B reálny `Prijímanie`.
- **Čo prevziať z ostatných:**
  - Pridať tag `Prijímanie`, druhý titul «Nohy jeleníc»; rozhodnúť `duši`/`ceste`.
- **Istota:** stredná – Delenie slôh je jasné, ale správne slovo nie.

**Riziká a neistoty:**

- Nie je overené, či `duši` alebo `ceste` je pôvodné znenie.

---

<a id="g30"></a>
## G30 · [4c] `Otváram srdce (MaranaTha).xml` · `Otváram srdce (...).xml` · `Srdce dokorán (Anonymous).xml`

**Zhrnutie:** Rovnaké slová (43 slov); súbory sa líšia poradím častí. C ukazuje plné poradie so zopakovanými slohami.

**Súbory v skupine:**
- **A** = `Otváram srdce (MaranaTha).xml`
- **B** = `Otváram srdce (...).xml`
- **C** = `Srdce dokorán (Anonymous).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B | C |
|---|---|---|---|
| Zodpovedá konvencii názvu | áno | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie | nie / nie |
| Tituly | `Otváram srdce` | `Otváram srdce` | `Srdce dokorán` |
| Tagy (`<author>`) | `MaranaTha` | `...` | `Anonymous` |
| songbooks | – | – | – |
| verseOrder | – | – | – |
| copyright / ccliNo | – / – | – / – | – / – |
| Slohy v poradí dokumentu | `v1 c1 v2 v3` | `c1 v1 c2` | `v1` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 3 / 3 | 1 / 1 |
| Počet riadkov (neprázdnych) | 13 (12) | 7 (7) | 24 (24) |
| Počet slov (bez čísel slôh) | 43 | 43 | 73 |
| verseOrder vs dokument | – | – | – |
| Slov po rozbalení verseOrder | 43 | 43 | 73 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 1 | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 4 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 | 5 / 0 |
| Konce riadkov súboru | LF | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 43 slov v A, 43 slov v B; 1 miest s rozdielom obsahu
1. [rovnaký text na inom mieste (iné poradie slôh)] A c1 r.1–2 a B c2 r.1: `So srdcom otvoreným znovu bežíme za tebou.`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 7, veľkosť písmen: 5
     - interpunkcia: A v1 r.1 `dokorán` vs B c1 r.1 `dokorán,`; A v1 r.2 `Duch` vs B c1 r.2 `Duch,`; A v1 r.3 `Duch` vs B c1 r.3 `Duch.`; A v2 r.3 `moc` vs B v1 r.2 `moc,`; A v2 r.4 `krok` vs B v1 r.2 `krok.`; A v3 r.2 `víťazí` vs B v1 r.3 `víťazí,`; A v3 r.3 `ísť` vs B v1 r.3 `ísť.`
     - veľkosť písmen: A v1 r.2 `tvoj` vs B c1 r.2 `Tvoj`; A v1 r.3 `Nech` vs B c1 r.3 `nech`; A v1 r.3 `tvoj` vs B c1 r.3 `Tvoj`; A v2 r.1 `ty` vs B v1 r.1 `Ty,`; A v3 r.1 `ty` vs B v1 r.3 `Ty,`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v B: –

*Dvojica A ↔ C:* 43 slov v A, 73 slov v C; 3 miest s rozdielom obsahu
2. [iný text] A c1 r.1–2: `So srdcom otvoreným znovu bežíme za tebou.`  vs  C v1 r.4: `<p/>`
3. [chýba v A] C v1 r.9: `<p/>` – v A tento text nie je
4. [chýba v A] C v1 r.13–24: `<p/> Tam, kde vstúpiš ty tma sa vytratí a strach už nemá moc ovládať … (35 slov)` – v A tento text nie je
   - Žiadne rozdiely v zápise (diakritika / veľkosť / interpunkcia) pri zhodných slovách.
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v C: `a`×2, `dáva`×1, `ísť`×1, `každý`×1, `kde`×2, `krok`×1, `láska`×1, `moc`×1, `nemá`×1, `ovládať`×1, `<p/>`×5, `sa`×1, `silu`×1, `strach`×1, `Tam,`×2, `tma`×1, `ty`×2, `už`×1, `víťazí`×1, `vládneš`×1, `vstúpiš`×1, `vytratí`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `MaranaTha` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1–2: `So srdcom otvoreným znovu bežíme za tebou.`
- **B**: tagy: `...` · tituly: – · text: nič unikátne
- **C**: tagy: `Anonymous` · tituly: `Srdce dokorán` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.4: `<p/>`; v1 r.9: `<p/>`; v1 r.13–22: `<p/> Tam, kde vstúpiš ty tma sa vytratí a strach už nemá moc ovládať každý krok … (28 slov)`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Otváram srdce (MaranaTha).xml` (A)
- **Zmazať / zlúčiť:** `Otváram srdce (...).xml` (B), `Srdce dokorán (Anonymous).xml` (C) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A a B majú rovnaký text (rozdiel 0 slov), C má 73 slov, pretože slohy `Tam, kde vstúpiš ty` / `Tam, kde vládneš ty` opakuje 2×.
  - Poradie v dokumente: A `v1 c1 v2 v3` (`So srdcom otvoreným` ako 2. časť), B `c1 v1 c2` (`So srdcom otvoreným` ako posledná), C: Otváram srdce → Tam, kde vstúpiš/vládneš → to isté znova → `So srdcom otvoreným` na konci. Bez `verseOrder` hrá A časti v inom poradí než C.
  - C je jedna 24-riadková sloha s 5 vloženými `<p/>`, B má značky `[: … :]` pri oboch refrénoch.
  - A má reálny tag `MaranaTha`, B a C len zástupné (`...`, `Anonymous`); C má iný titul `Srdce dokorán`.
- **Čo prevziať z ostatných:**
  - Do A doplniť `verseOrder` «v1 v2 v3 v2 v3 c1» (podľa poradia v C), druhý titul «Srdce dokorán».
- **Istota:** stredná – Text je rovnaký; správne poradie hrania vyplýva len z C.

**Riziká a neistoty:**

- Poradie podľa C nie je overené inak; B navrhuje refrén `Otváram srdce` hneď na začiatku s opakovaním `[: :]`.

---

<a id="g31"></a>
## G31 · [4c] `Pane, som tak veľmi rád (Veľkonočná).xml` · `Pane, som tak veľmi rád (Anonymous).xml`

**Zhrnutie:** Obsah takmer rovnaký; A má `aj` navyše a preklep `musels`, B má štruktúru `c1` a prázdny riadok na konci.

**Súbory v skupine:**
- **A** = `Pane, som tak veľmi rád (Veľkonočná).xml`
- **B** = `Pane, som tak veľmi rád (Anonymous).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Pane, som tak veľmi rád` | `Pane, som tak veľmi rád` |
| Tagy (`<author>`) | `Veľkonočná` | `Anonymous` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2` | `v1 c1` |
| Počet slôh / `<lines>` blokov | 2 / 2 | 2 / 2 |
| Počet riadkov (neprázdnych) | 9 (9) | 7 (6) |
| Počet slov (bez čísel slôh) | 56 | 55 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 56 | 55 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 1 |
| Prázdne riadky (`<br/><br/>`) | 0 | 1 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 1 | 1 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 56 slov v A, 55 slov v B; 1 miest s rozdielom obsahu
1. [chýba v B] A v2 r.2: `aj` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 6, interpunkcia: 2
     - veľkosť písmen: A v1 r.2 `Tebou` vs B v1 r.1 `tebou`; A v1 r.3 `tak` vs B v1 r.2 `Tak`; A v1 r.3 `Ti` vs B v1 r.2 `ti`; A v1 r.4 `Teba` vs B v1 r.2 `teba`; A v2 r.4 `Ťa` vs B c1 r.4 `ťa`; A v2 r.5 `Ti` vs B c1 r.4 `ti`
     - interpunkcia: A v1 r.2 `skúsil,` vs B v1 r.1 `skúsil.`; A v2 r.2 `musels` vs B c1 r.2 `musel´s`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `aj`×1; viac v B: –

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Veľkonočná` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.2: `aj`
- **B**: tagy: `Anonymous` · tituly: – · text: nič unikátne

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Pane, som tak veľmi rád (Veľkonočná).xml` (A)
- **Zmazať / zlúčiť:** `Pane, som tak veľmi rád (Anonymous).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Jediný slovný rozdiel: A `tu na kríži musels  mrieť aj za môj hriech.` (v2 r.2) vs B `tu na kríži musel´s mrieť za môj hriech.` (c1 r.2) – slovo `aj` má iba A; skrátené „musel si“ píše A ako `musels` (preklep) a B ako `musel´s`.
  - B má v1 s dlhými riadkami a trojitými medzerami (`Pane, som tak veľmi rád,   život s tebou som už skúsil.`) a prázdny riadok na konci `c1`; A má kratšie riadky a žiadny prázdny riadok.
  - A má reálny tag `Veľkonočná`; B len zástupný `Anonymous`.
- **Čo prevziať z ostatných:**
  - V A opraviť `musels` na «musel’s» (alebo na „musel si“); voliteľne premenovať `v2` na `c1`.
- **Istota:** vysoká – Rozdiel je len formát a jedno slovo `aj`.

**Riziká a neistoty:**

- Slovo `aj` (A) nie je overené inde.

---

<a id="g32"></a>
## G32 · [4c] `Poď, teraz je čas (Začiatok).xml` · `Pod, teraz je cas vzdat chvalu (detsky zbor).xml`

**Zhrnutie:** Rovnaký text; A má v názve nezlomiteľné medzery, B titul bez diakritiky a natiahnutú slabiku `dá-áš.`

Existuje aj verzia s akordmi: `Pod, teraz je cas vzdat chvalu (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Poď, teraz je čas (Začiatok).xml`
- **B** = `Pod, teraz je cas vzdat chvalu (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | áno / áno | nie / nie |
| Tituly | `Poď, teraz je čas` | `Pod, teraz je cas vzdat chvalu` |
| Tagy (`<author>`) | `Začiatok` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | `v1 c1 v2` |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3` | `v1 v2 c1` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 3 / 3 |
| Počet riadkov (neprázdnych) | 12 (12) | 10 (10) |
| Počet slov (bez čísel slôh) | 67 | 66 |
| verseOrder vs dokument | – | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 67 | 66 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 2 | 2 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | CRLF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 67 slov v A, 66 slov v B; 2 miest s rozdielom obsahu
1. [chýba v A] B v1 r.4 – v2 r.2: `Poď! Poď, teraz je čas vzdať chválu, poď, srdce svoje mu s láskou daj.` – v A tento text nie je
2. [iný text] A v2 r.4 – v3 r.3: `dáš. Poď, teraz je čas vzdať chválu. Poď, srdce svoje mu s láskou daj. … (16 slov)`  vs  B c1 r.4: `dá-áš.`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 6, veľkosť písmen: 6, značky opakovania: 1
     - interpunkcia: A v1 r.1 `chválu.` vs B v1 r.1 `chválu,`; A v1 r.3 `Poď` vs B v1 r.3 `Poď,`; A v1 r.3 `taký,` vs B v1 r.3 `taký`; A v1 r.3 `si,` vs B v1 r.3 `si`; A v1 r.4 `Kráľa,` vs B v1 r.4 `Kráľa`; A v2 r.1 `Pán.` vs B c1 r.1 `Pán!`
     - veľkosť písmen: A v1 r.2 `Poď,` vs B v1 r.2 `poď,`; A v1 r.3 `ho.` vs B v1 r.3 `Ho,`; A v1 r.4 `Poď,` vs B v1 r.4 `poď,`; A v2 r.2 `ti` vs B c1 r.2 `Ti`; A v2 r.3 `ťa` vs B c1 r.3 `Ťa`; A v2 r.4 `ty` vs B c1 r.4 `Ty`
     - značky opakovania: A v2 r.1 `Každý` vs B c1 r.1 `/:Každý`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `dáš.`×1, `Tak`×1; viac v B: `dá-áš.`×1
   - V poradí hrania (po rozbalení verseOrder): 67 vs 66 slov, 2 miest s rozdielom obsahu: A `Tak` vs B ``; A `dáš.` vs B `dá-áš.`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Začiatok` · tituly: `Poď, teraz je čas` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.4 – v3 r.3: `dáš. Poď, teraz je čas vzdať chválu. Poď, srdce svoje mu s láskou daj. Tak poď!`
- **B**: tagy: `detsky zbor` · tituly: `Pod, teraz je cas vzdat chvalu` · verseOrder `v1 c1 v2` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.4 – v2 r.2: `Poď! Poď, teraz je čas vzdať chválu, poď, srdce svoje mu s láskou daj.`; c1 r.4: `dá-áš.`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Poď, teraz je čas (Začiatok).xml` (A)
- **Zmazať / zlúčiť:** `Pod, teraz je cas vzdat chvalu (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Slovný rozdiel je len `Tak poď!` (A, v1 r.5) vs `Poď!` (B, v1 r.4) a `dáš.` vs `dá-áš.` (B, c1 r.4).
  - A hrá `v1 v2 v3` v poradí dokumentu, B má `verseOrder` `v1 c1 v2` – po rozbalení sa líšia len v 2 miestach (`Tak` a `dá-áš.`).
  - A má titul aj názov súboru s nezlomiteľnými medzerami (`Poď, teraz je čas`); B má titul `Pod, teraz je cas vzdat chvalu`.
  - B nemá unikátny text ani tag okrem `detsky zbor`.
- **Čo prevziať z ostatných:**
  - V A nahradiť nezlomiteľné medzery bežnými (premenovanie súboru); pridať tag `detsky zbor`.
- **Istota:** vysoká – Obsah je takmer totožný.

**Riziká a neistoty:**

- Premenovaním A zanikne položka v zozname súborov s nezlomiteľnou medzerou (duplicity.md, časť 6).

---

<a id="g33"></a>
## G33 · [4c] `Poďme všetci spolu (Rieka Života).xml` · `podme vsetci spolu (detský zbor).xml` · `podme chvalit ho (Anonymous).xml`

**Zhrnutie:** Slohy majú rovnaký text; C má navyše koncovku `Poďme chváliť ho` / `Ježiš` 4×, B má iné poradie častí.

**Súbory v skupine:**
- **A** = `Poďme všetci spolu (Rieka Života).xml`
- **B** = `podme vsetci spolu (detský zbor).xml`
- **C** = `podme chvalit ho (Anonymous).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B | C |
|---|---|---|---|
| Zodpovedá konvencii názvu | áno | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie | nie / nie |
| Tituly | `Poďme všetci spolu` | `podme vsetci spolu` | `podme chvalit ho` |
| Tagy (`<author>`) | `Rieka Života` | `detský zbor` | `Anonymous` |
| songbooks | – | – | – |
| verseOrder | – | – | – |
| copyright / ccliNo | – / – | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 c1 c2 v3 v4` | `v1a v2 v1b` | `v1 c1 v2 o1` |
| Počet slôh / `<lines>` blokov | 6 / 6 | 3 / 3 | 4 / 4 |
| Počet riadkov (neprázdnych) | 24 (24) | 17 (12) | 20 (20) |
| Počet slov (bez čísel slôh) | 72 | 72 | 88 |
| verseOrder vs dokument | – | – | – |
| Slov po rozbalení verseOrder | 72 | 72 | 88 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 5 | 0 |
| Riadky s koncovou medzerou | 6 | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 72 slov v A, 72 slov v B; 1 miest s rozdielom obsahu
1. [rovnaký text na inom mieste (iné poradie slôh)] A v3 r.1 – v4 r.4 a B v2 r.2–5: `Povstaň Božie vojsko, je čas začať boj, Spievajme hosana, poďme … (21 slov)`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 8
     - interpunkcia: A v1 r.2 `hlas,` vs B v1a r.1 `hlas`; A v1 r.4 `zrak.` vs B v1a r.2 `zrak`; A v2 r.2 `vrch,` vs B v1a r.3 `vrch`; A v2 r.4 `ho.` vs B v1a r.4 `ho`; A c1 r.2 `ho,` vs B v1b r.1 `ho`; A c1 r.4 `ho.` vs B v1b r.2 `ho`; A c2 r.2 `zazvoní,` vs B v1b r.3 `zazvoní`; A c2 r.4 `ho.` vs B v1b r.4 `ho`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v B: –

*Dvojica A ↔ C:* 72 slov v A, 88 slov v C; 1 miest s rozdielom obsahu
2. [chýba v A] C o1 r.1–8: `Poďme chváliť ho Ježiš Poďme chváliť ho Ježiš Poďme chváliť ho Ježiš Poďme chváliť … (16 slov)` – v A tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 12
     - interpunkcia: A v1 r.2 `hlas,` vs C v1 r.1 `hlas`; A v1 r.4 `zrak.` vs C v1 r.2 `zrak`; A v2 r.2 `vrch,` vs C v1 r.3 `vrch`; A v2 r.4 `ho.` vs C v1 r.4 `ho`; A c1 r.2 `ho,` vs C c1 r.1 `ho`; A c1 r.4 `ho.` vs C c1 r.2 `ho`; A c2 r.2 `zazvoní,` vs C c1 r.3 `zazvoní`; A c2 r.4 `ho.` vs C c1 r.4 `ho` … (+4)
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v C: `chváliť`×4, `ho.`×4, `Ježiš`×4, `Poďme`×4

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Rieka Života` · tituly: `Poďme všetci spolu` · text: nič unikátne
- **B**: tagy: `detský zbor` · tituly: `podme vsetci spolu` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.2–5: `Povstaň Božie vojsko, je čas začať boj Spievajme hosana, poďme chváliť ho Nepriateľa zničí, vraha porazí … (21 slov)`
- **C**: tagy: `Anonymous` · tituly: `podme chvalit ho` · text (slová, ktoré v žiadnom inom súbore nie sú): o1 r.1–8: `Poďme chváliť ho Ježiš Poďme chváliť ho Ježiš Poďme chváliť ho Ježiš Poďme chváliť ho Ježiš`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Poďme všetci spolu (Rieka Života).xml` (A)
- **Zmazať / zlúčiť:** `podme vsetci spolu (detský zbor).xml` (B), `podme chvalit ho (Anonymous).xml` (C) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Všetky tri majú rovnaký text slôh (72 slov); C má koncovku `o1`: `Poďme chváliť ho` / `Ježiš` 4× (16 slov), ktorú nemá A ani B.
  - Poradie: A `v1 v2 c1 c2 v3 v4` a C (v1, c1, v2) sú rovnaké; B má poradie (A v1+v2) → (A v3+v4) → (A c1+c2), teda refrén až na konci.
  - B má 5 prázdnych riadkov, titul bez diakritiky `podme vsetci spolu` a tag `detský zbor` (s „ý“, odlišný od používaného `detsky zbor`).
  - A má reálny tag `Rieka Života`, C len zástupný `Anonymous`.
- **Čo prevziať z ostatných:**
  - Pridať tag `detsky zbor`; rozhodnúť, či sa koncovka z C (o1) má pridať ako sloha `e1`.
- **Istota:** stredná – Keeper A je jasný; otvorená je len koncovka C.

**Riziká a neistoty:**

- Koncovka z C je jediný unikátny text v skupine; nevieme, či patrí k piesni.

---

<a id="g34"></a>
## G34 · [4c] `Prijmi tieto naše dary, Pane (Obetné dary).xml` · `Príjmi tieto naše dary (detsky zbor).xml`

**Zhrnutie:** B nemá 3. slohu a má niekoľko odlišných slov (`všetkých`, `teba` na inom mieste); A je úplnejšia.

**Súbory v skupine:**
- **A** = `Prijmi tieto naše dary, Pane (Obetné dary).xml`
- **B** = `Príjmi tieto naše dary (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | áno / áno | nie / nie |
| Tituly | `Prijmi tieto naše dary, Pane` | `Príjmi tieto naše dary` |
| Tagy (`<author>`) | `Obetné dary` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3` | `v1 v2` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 2 / 2 |
| Počet riadkov (neprázdnych) | 12 (12) | 5 (4) |
| Počet slov (bez čísel slôh) | 71 | 45 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 71 | 45 |
| Riadky s číslom slohy na začiatku (`1.`) | 3 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 1 |
| Riadky s koncovou medzerou | 0 | 1 |
| Riadky s dvojitou medzerou vnútri | 0 | 2 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 71 slov v A, 45 slov v B; 5 miest s rozdielom obsahu
1. [chýba v B] A v1 r.2: `v` – v B tento text nie je
2. [iný text] A v2 r.1: `mladých,`  vs  B v2 r.2: `všetkých,`
     - riadok v A: `2. Táto obeť je obetou mladých,`
     - riadok v B: `Táto obeť je obetou všetkých,  ktorí chcú svoj život obnoviť.`
3. [iný text] A v2 r.4: `Teba,`  vs  B v2 r.3: `nikto,`
     - riadok v A: `Teba, Pane, nemôže nikto nahradiť.`
     - riadok v B: `Podľa tvojich príkazov vždy chcú žiť, nikto, Pane, nemôže teba nahradiť.`
4. [iný text] A v2 r.4: `nikto`  vs  B v2 r.3: `teba`
     - riadok v A: `Teba, Pane, nemôže nikto nahradiť.`
     - riadok v B: `Podľa tvojich príkazov vždy chcú žiť, nikto, Pane, nemôže teba nahradiť.`
5. [chýba v B] A v3 r.1–4: `Dobre je nám s Tebou v Tvojom chráme, mnohí Ťa však vonku hľadajú. Prosíme … (25 slov)` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 2
     - veľkosť písmen: A v1 r.4 `Tebe.` vs B v1 r.2 `tebe.`; A v2 r.3 `Tvojich` vs B v2 r.3 `tvojich`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `bojoch`×1, `cez`×1, `chráme,`×1, `Dobre`×1, `hľadajú.`×1, `je`×1, `každodenných`×1, `mladých,`×1, `mnohí`×1, `nám`×2, `nás`×1, `Nech`×1, `pomáhaj`×1, `Prosíme`×1, `s`×1, `spoznajú`×1, `Ťa`×2, `Teba,`×1, `Tebou`×1, `Tvojom`×1, `v`×3, `vonku`×1, `však`×1; viac v B: `všetkých,`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Obetné dary` · tituly: `Prijmi tieto naše dary, Pane` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.2: `v`; v2 r.1: `mladých,`; v2 r.4: `Teba,`; v2 r.4: `nikto`; v3 r.1–4: `Dobre je nám s Tebou v Tvojom chráme, mnohí Ťa však vonku hľadajú. Prosíme Ťa, pomáhaj … (25 slov)`
- **B**: tagy: `detsky zbor` · tituly: `Príjmi tieto naše dary` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.2: `všetkých,`; v2 r.3: `nikto,`; v2 r.3: `nahradiť.`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Prijmi tieto naše dary, Pane (Obetné dary).xml` (A)
- **Zmazať / zlúčiť:** `Príjmi tieto naše dary (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A má 3 slohy (71 slov), B len 2 (45 slov); chýba jej `Dobre je nám s Tebou v Tvojom chráme, mnohí Ťa však vonku hľadajú.` (A, v3).
  - Slovné varianty: A `Táto obeť je obetou mladých,` vs B `Táto obeť je obetou všetkých,`; A `Teba, Pane, nemôže nikto nahradiť.` vs B `nikto, Pane, nemôže teba nahradiť.`; A `vo víne a v chlebe` vs B `vo víne a chlebe`.
  - A má v titule aj názve súboru nezlomiteľné medzery (`Prijmi tieto naše dary, Pane`); B má titul `Príjmi tieto naše dary`.
  - B nemá unikátny text okrem uvedených variantov a tagu `detsky zbor`.
- **Čo prevziať z ostatných:**
  - Pridať tag `detsky zbor`; rozhodnúť, či sa varianty `všetkých` a `nikto, Pane, nemôže teba nahradiť` majú zachovať.
- **Istota:** stredná – A je úplnejšia, ale B môže byť zámerne upravené znenie pre iné použitie.

**Riziká a neistoty:**

- Variant `všetkých` môže byť zovšeobecnenie pre iné použitie než mládež.

---

<a id="g35"></a>
## G35 · [4c] `Si môj Pán, Ježiš Kráľ (Author Unknown).xml` · `si moj pan (Author Unknown).xml`

**Zhrnutie:** Rovnaký text, ale B má na 15 miestach slová s chybnou diakritikou alebo preklepom.

**Súbory v skupine:**
- **A** = `Si môj Pán, Ježiš Kráľ (Author Unknown).xml`
- **B** = `si moj pan (Author Unknown).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Si môj Pán, Ježiš Kráľ` | `si moj pan` |
| Tagy (`<author>`) | `Author Unknown` | `Author Unknown` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3` | `v1 v2 v3 c1` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 4 / 4 |
| Počet riadkov (neprázdnych) | 15 (15) | 10 (10) |
| Počet slov (bez čísel slôh) | 87 | 63 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 87 | 63 |
| Riadky s číslom slohy na začiatku (`1.`) | 3 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 6 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 87 slov v A, 63 slov v B; 4 miest s rozdielom obsahu
1. [chýba v B] A v1 r.1–2: `Si môj Pán, Ježiš Kráľ, každý deň sa zhováram s tebou rád.` – v B tento text nie je
2. [chýba v B] A v2 r.1–2: `Si môj Pán, Ježiš Kráľ, každý deň sa zhováram s tebou rád.` – v B tento text nie je
3. [preklep / zmena slova] A v3 r.2: `tebou`  vs  B c1 r.2: `tebov`
     - riadok v A: `každý deň sa zhováram s tebou rád.`
     - riadok v B: `každý deň sa zhováram s tebov rád`
4. [rovnaký text na inom mieste (iné poradie slôh)] A v3 r.3–5 a B v3 r.1–3: `Ty si vtáčkom piesne dal, aby som sa radoval, si … (16 slov)`
     - v presunutom úseku: A `vtáčkom` vs B `vtakom`
     - v presunutom úseku: A `kamarát,` vs B `kamarad,`
   - Rozdiely len v zápise (rovnaké slová): diakritika: 8, diakritika + veľkosť písmen: 1, interpunkcia: 1
     - diakritika: A v1 r.4 `celý` vs B v1 r.1 `cely`; A v1 r.5 `náš` vs B v1 r.2 `naš`; A v1 r.5 `mám` vs B v1 r.2 `mam`; A v1 r.5 `rád.` vs B v1 r.2 `rad.`; A v2 r.4 `každý` vs B v2 r.2 `každy`; A v2 r.5 `toľkokrát,` vs B v2 r.3 `tolkokrat,`; A v2 r.5 `mám` vs B v2 r.3 `mam`; A v2 r.5 `rád.` vs B v2 r.3 `rad.`
     - diakritika + veľkosť písmen: A v3 r.1 `Kráľ,` vs B c1 r.1 `kraľ,`
     - interpunkcia: A v3 r.2 `rád.` vs B c1 r.2 `rád`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `deň`×2, `Ježiš`×2, `kamarát,`×1, `každý`×2, `Kráľ,`×2, `môj`×2, `Pán,`×2, `rád.`×2, `s`×2, `sa`×2, `Si`×2, `tebou`×3, `vtáčkom`×1, `zhováram`×2; viac v B: `kamarad,`×1, `tebov`×1, `vtakom`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: – · tituly: `Si môj Pán, Ježiš Kráľ` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1–2: `Si môj Pán, Ježiš Kráľ, každý deň sa zhováram s tebou rád.`; v2 r.1–2: `Si môj Pán, Ježiš Kráľ, každý deň sa zhováram s tebou rád.`; v3 r.2: `tebou`; v3 r.3–5: `Ty si vtáčkom piesne dal, aby som sa radoval, si môj verný kamarát, mám ťa rád.`
- **B**: tagy: – · tituly: `si moj pan` · text (slová, ktoré v žiadnom inom súbore nie sú): v3 r.1–3: `Ty si vtakom piesne dal, aby som sa radoval, si môj verny kamarad, mam ťa rad.`; c1 r.2: `tebov`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Si môj Pán, Ježiš Kráľ (Author Unknown).xml` (A)
- **Zmazať / zlúčiť:** `si moj pan (Author Unknown).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B píše s chybami v diakritike: `cely svet`, `naš sad`, `mam ťa rad`, `každy hriech`, `tolkokrat`, `vtakom`, `verny kamarad`, `kraľ` a `tebov rád`; A má na týchto miestach `celý svet`, `náš sad`, `mám ťa rád`, `každý hriech`, `toľkokrát`, `vtáčkom`, `verný kamarát`, `Kráľ` a `tebou rád`.
  - A má na začiatku každej slohy riadky `Si môj Pán, Ježiš Kráľ,` / `každý deň sa zhováram s tebou rád.` (3×); B ich má raz v `c1` na konci a nemá `verseOrder`.
  - Titul B je `si moj pan`, A `Si môj Pán, Ježiš Kráľ`; obaja majú zástupný tag `Author Unknown`, takže sa nič nestratí.
- **Čo prevziať z ostatných:** nič.
- **Istota:** vysoká – B je horšia verzia toho istého textu.

**Riziká a neistoty:**

- Štruktúra B (refrén raz ako `c1`) je kompaktnejšia; ak sa preferuje, treba upraviť A.

---

<a id="g36"></a>
## G36 · [4c] `Stretol ma dnes Pán (Prijímanie, Veľkonočná).xml` · `Tak všetci spolu chváľme ho (detsky zbor).xml`

*Poznámka: `duplicity.md` uvádza pri tejto skupine aj kópie, ktoré už neexistujú (už zlúčené); porovnávané sú len súbory uvedené vyššie.*

**Zhrnutie:** B má navyše `Ó aleluja,` a refrén ako `c1`; A má reálne tagy `Prijímanie`, `Veľkonočná`, ktoré treba preniesť.

**Súbory v skupine:**
- **A** = `Stretol ma dnes Pán (Prijímanie, Veľkonočná).xml`
- **B** = `Tak všetci spolu chváľme ho (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Stretol ma dnes Pán` | `Tak všetci spolu chváľme ho`<br>`Stretol ma dnes Pán` |
| Tagy (`<author>`) | `Prijímanie`, `Veľkonočná` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1` | `v1 c1` |
| Počet slôh / `<lines>` blokov | 1 / 1 | 2 / 2 |
| Počet riadkov (neprázdnych) | 6 (6) | 4 (4) |
| Počet slov (bez čísel slôh) | 31 | 33 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 31 | 33 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 1 | 2 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica B ↔ A:* 33 slov v B, 31 slov v A; 1 miest s rozdielom obsahu
1. [chýba v A] B v1 r.2: `Ó aleluja,` – v A tento text nie je
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 2, interpunkcia: 2
     - veľkosť písmen: B v1 r.2 `z` vs A v1 r.3 `Z`; B c1 r.1 `ho,` vs A v1 r.5 `Ho`
     - interpunkcia: B v1 r.2 `chcem,` vs A v1 r.3 `chcem`; B c1 r.2 `náručí` vs A v1 r.6 `náručí.`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v B: `aleluja,`×1, `Ó`×1; viac v A: –

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Prijímanie`, `Veľkonočná` · tituly: – · text: nič unikátne
- **B**: tagy: `detsky zbor` · tituly: `Tak všetci spolu chváľme ho` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.2: `Ó aleluja,`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Tak všetci spolu chváľme ho (detsky zbor).xml` (B)
- **Zmazať / zlúčiť:** `Stretol ma dnes Pán (Prijímanie, Veľkonočná).xml` (A) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B obsahuje slová `Ó aleluja,` (v1 r.2: `Ó aleluja, z tej radosti chcem, spievať a tlieskať Pánovi.`), ktoré A nemá.
  - B ukladá refrén ako samostatnú sloha `c1` so značkami `[: Tak všetci spolu chváľme ho,` … `v náručí :]`; A má jednu 6-riadkovú sloha a koncovú značku s medzerou `v náručí. : |`.
  - B už obsahuje oba tituly po predošlom zlúčení: `Tak všetci spolu chváľme ho` a `Stretol ma dnes Pán`.
  - A má reálne tagy `Prijímanie`, `Veľkonočná`; B len `detsky zbor`.
- **Čo prevziať z ostatných:**
  - Do B pridať tagy `Prijímanie`, `Veľkonočná`; voliteľne preusporiadať tituly, aby prvý bol `Stretol ma dnes Pán`.
- **Istota:** stredná – Rozhoduje, či `Ó aleluja,` patrí do pôvodného textu (je len v B).

**Riziká a neistoty:**

- Slová `Ó aleluja,` nie sú overené žiadnou referenciou.
- A má kratšie riadky vhodnejšie na slajdy (B má 2 dlhé riadky v `v1`).

---

<a id="g37"></a>
## G37 · [4c] `Svätý (Večeradlo s Pannou Máriou).xml` · `Svaty - Pane Boze svetov nekonecnych (detsky zbor).xml`

**Zhrnutie:** Rovnaký text; A píše Hosanu dvakrát v strede a na konci, B raz ako `c1` s `verseOrder` `v1 v2 c1 c1`.

Existuje aj verzia s akordmi: `Svaty - Pane Boze svetov nekonecnych (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Svätý (Večeradlo s Pannou Máriou).xml`
- **B** = `Svaty - Pane Boze svetov nekonecnych (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Svätý` | `Svaty - Pane Boze svetov nekonecnych` |
| Tagy (`<author>`) | `Večeradlo s Pannou Máriou` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | `v1 v2 c1 c1` |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3` | `v1 v2 c1` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 3 / 3 |
| Počet riadkov (neprázdnych) | 10 (10) | 4 (4) |
| Počet slov (bez čísel slôh) | 38 | 30 |
| verseOrder vs dokument | – | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 38 | 36 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 1 | 0 |
| Riadky s dvojitou medzerou vnútri | 1 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 4 | 2 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 38 slov v A, 30 slov v B; 3 miest s rozdielom obsahu
1. [iný text] A v1 r.1: `Svätý, svätý, svätý,`  vs  B v1 r.1: `Svätý,svätý,svätý,`
     - riadok v A: `Svätý,  svätý,  svätý,`
     - riadok v B: `Svätý,svätý,svätý, Pane Bože svetov nekonečných.`
2. [chýba v B] A v2 r.1–2: `[:Hosana, hosana, hosana buď Kráľovi kráľov.:]` – v B tento text nie je
3. [iný text] A v3 r.2: `[:Hosana, hosana, hosana`  vs  B c1 r.1: `/:Hosanna, Hosanna, Hosanna`
     - riadok v A: `[:Hosana, hosana, hosana`
     - riadok v B: `/:Hosanna, Hosanna, Hosanna buď Kráľovi kráľov.:/`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 1, veľkosť písmen: 1, značky opakovania: 1
     - interpunkcia: A v1 r.2 `nekonečných` vs B v1 r.1 `nekonečných.`
     - veľkosť písmen: A v1 r.3 `si` vs B v1 r.2 `Si`
     - značky opakovania: A v3 r.3 `kráľov.:]` vs B c1 r.1 `kráľov.:/`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `buď`×1, `[:Hosana,`×6, `kráľov.:]`×1, `Kráľovi`×1, `Svätý,`×3; viac v B: `/:Hosanna,`×3, `Svätý,svätý,svätý,`×1
   - V poradí hrania (po rozbalení verseOrder): 38 vs 36 slov, 3 miest s rozdielom obsahu: A `Svätý, svätý, svätý,` vs B `Svätý,svätý,svätý,`; A `[:Hosana, hosana, hosana buď Kráľovi kráľov.:]` vs B `/:Hosanna, Hosanna, Hosanna buď Kráľovi kráľov.:/`; A `[:Hosana, hosana, hosana` vs B `/:Hosanna, Hosanna, Hosanna`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Večeradlo s Pannou Máriou` · tituly: `Svätý` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1: `Svätý, svätý, svätý,`; v2 r.1–2: `[:Hosana, hosana, hosana buď Kráľovi kráľov.:]`; v3 r.2: `[:Hosana, hosana, hosana`
- **B**: tagy: `detsky zbor` · tituly: `Svaty - Pane Boze svetov nekonecnych` · verseOrder `v1 v2 c1 c1` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1: `Svätý,svätý,svätý,`; c1 r.1: `/:Hosanna, Hosanna, Hosanna`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Svätý (Večeradlo s Pannou Máriou).xml` (A)
- **Zmazať / zlúčiť:** `Svaty - Pane Boze svetov nekonecnych (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A má blok `[:Hosana, hosana, hosana` / `buď Kráľovi kráľov.:]` v `v2` aj v `v3` (medzi Svätý a `V mene Pánovom` a na konci); B ho má raz v `c1`: `/:Hosanna, Hosanna, Hosanna buď Kráľovi kráľov.:/`.
  - B má `verseOrder` `v1 v2 c1 c1` – po rozbalení sa Hosanna zopakuje dvakrát za sebou na konci a prvá Hosanna po `v1` chýba (36 slov oproti 38 v A).
  - Pravopis: A `Hosana`, B `Hosanna`; A má dvojité medzery `Svätý,  svätý,  svätý,` (v1 r.1) a B zlepené `Svätý,svätý,svätý,`.
  - A má reálny tag `Večeradlo s Pannou Máriou`, B len `detsky zbor`; titul B je bez diakritiky `Svaty - Pane Boze svetov nekonecnych`.
- **Čo prevziať z ostatných:**
  - Pridať tag `detsky zbor`; rozhodnúť pravopis `Hosana`/`Hosanna`.
- **Istota:** stredná – Text je rovnaký, ale správne poradie Hosanny sa nedá overiť.

**Riziká a neistoty:**

- Ak je poradie v B zámerné (dva refrény za sebou), zmazaním B sa stratí.

---

<a id="g38"></a>
## G38 · [4c] `Svoj pokoj (...).xml` · `Svoj pokoj (Anonymous).xml`

**Zhrnutie:** B má v poslednej slohe preklep `spoj` a chýba jej slovo `ja`.

**Súbory v skupine:**
- **A** = `Svoj pokoj (...).xml`
- **B** = `Svoj pokoj (Anonymous).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Svoj pokoj` | `Svoj pokoj` |
| Tagy (`<author>`) | `...` | `Anonymous` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1` | `v1 v2 v3 v4` |
| Počet slôh / `<lines>` blokov | 1 / 1 | 4 / 4 |
| Počet riadkov (neprázdnych) | 4 (4) | 8 (8) |
| Počet slov (bez čísel slôh) | 37 | 36 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 37 | 36 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 1 | 4 |
| Riadky s dvojitou medzerou vnútri | 0 | 1 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 37 slov v A, 36 slov v B; 2 miest s rozdielom obsahu
1. [chýba v B] A v1 r.4: `ja` – v B tento text nie je
2. [preklep / zmena slova] A v1 r.4: `svoj`  vs  B v4 r.2: `spoj`
     - riadok v A: `Svoj pokoj vám ja zanechávam, svoj pokoj vám dávam.`
     - riadok v B: `spoj pokoj vám dávam.`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 1
     - interpunkcia: A v1 r.2 `svet;` vs B v2 r.1 `svet,`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `ja`×1, `Svoj`×1; viac v B: `spoj`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `...` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.4: `ja`; v1 r.4: `svoj`
- **B**: tagy: `Anonymous` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): v4 r.2: `spoj`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Svoj pokoj (...).xml` (A)
- **Zmazať / zlúčiť:** `Svoj pokoj (Anonymous).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B v4 r.1–2: `Svoj pokoj vám zanechávam,` / `spoj pokoj vám dávam.` – chýba `ja` a je tam preklep `spoj`; A má `Svoj pokoj vám ja zanechávam, svoj pokoj vám dávam.`
  - Obsah ostatných riadkov je rovnaký; B ho len delí do 4 slôh po 2 riadkoch (A: 1 sloha so 4 riadkami).
  - Oba majú zástupný tag (`...` v A, `Anonymous` v B), takže sa nič nestratí; B má 4 riadky s koncovou medzerou.
- **Čo prevziať z ostatných:** nič.
- **Istota:** vysoká – B je horšia kópia toho istého textu.

**Riziká a neistoty:**

- Delenie B na 4 slohy po 2 riadkoch môže vyhovovať zobrazeniu (kratšie slajdy).

---

<a id="g39"></a>
## G39 · [4c] `Šťastie (Mariánska).xml` · `Je dnes taký zvláštne krásny deň (Mariánska).xml`

**Zhrnutie:** B nemá 3. slohu, ale má opravené preklepy (`tvári`, `nenájde`) a `verseOrder`; A je úplná, ale s preklepmi.

**Súbory v skupine:**
- **A** = `Šťastie (Mariánska).xml`
- **B** = `Je dnes taký zvláštne krásny deň (Mariánska).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Šťastie` | `Je dnes taký zvláštne krásny deň` |
| Tagy (`<author>`) | `Mariánska` | `Mariánska` |
| songbooks | – | – |
| verseOrder | – | `v1 v2 v3 v2` |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4` | `v1 v2 v3` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 3 / 3 |
| Počet riadkov (neprázdnych) | 26 (26) | 18 (18) |
| Počet slov (bez čísel slôh) | 139 | 98 |
| verseOrder vs dokument | – | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 139 | 108 |
| Riadky s číslom slohy na začiatku (`1.`) | 3 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 139 slov v A, 98 slov v B; 5 miest s rozdielom obsahu
1. [preklep / zmena slova] A v1 r.5: `tváti,`  vs  B v1 r.5: `tvári,`
     - riadok v A: `Šťastie, to je úsmev na tváti,`
     - riadok v B: `Šťastie to je úsmev na tvári,`
2. [pokyn v texte] A v2 r.1: `R.` – v B tento text nie je
3. [preklep / zmena slova] A v3 r.5: `nanájde,`  vs  B v3 r.5: `nenájde,`
     - riadok v A: `Hľadá šťastie, ktoré nanájde,`
     - riadok v B: `Hľadá šťastie, ktoré nenájde,`
4. [iný text] A v3 r.7: `byť,`  vs  B v3 r.7: `žiť,`
     - riadok v A: `On musí pochopiť, že s Máriou byť,`
     - riadok v B: `On musí pochopiť, že s Máriou žiť,`
5. [chýba v B] A v4 r.1–8: `Skúsme sa častejšia pomodliť, skúsme nežne teplo pocítiť, ktoré zavanie v našich srdiečkach a … (40 slov)` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 7, veľkosť písmen: 2
     - interpunkcia: A v1 r.1 `deň,` vs B v1 r.1 `deň`; A v1 r.3 `rozjasní,` vs B v1 r.3 `rozjasní`; A v1 r.5 `Šťastie,` vs B v1 r.5 `Šťastie`; A v1 r.7 `poteší,` vs B v1 r.7 `poteší`; A v3 r.2 `otázku,` vs B v3 r.2 `otázku`; A v3 r.3 `zlý,` vs B v3 r.3 `zlý`; A v3 r.6 `nerastie.` vs B v3 r.6 `nerastie,`
     - veľkosť písmen: A v1 r.7 `mamke,` vs B v1 r.7 `Mamke,`; A v2 r.2 `mamka` vs B v2 r.2 `Mamka`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `a`×2, `byť`×1, `častejšia`×1, `čo`×1, `duší`×1, `ktoré`×1, `len`×1, `ľudia`×1, `Máriou`×1, `nám`×1, `nanájde,`×1, `našich`×1, `nechceme`×1, `nenávisť,`×1, `nežne`×1, `nie`×1, `nikdy`×1, `odoženie`×1, `pocítiť,`×1, `pokúsme`×1, `pomodliť,`×1, `pozrime,`×1, `R.`×1, `robí.`×1, `s`×1, `sa`×2, `si`×1, `skúsme`×2, `srdiečkach`×1, `strach.`×1, `svedomie,`×1, `teplo`×1, `tváti,`×1, `už`×1, `v`×1, `vedomie,`×1, `z`×1, `zavanie`×1, `zlosť`×1, `Zoberme`×1; viac v B: `nenájde,`×1, `tvári,`×1
   - V poradí hrania (po rozbalení verseOrder): 139 vs 108 slov, 5 miest s rozdielom obsahu: A `tváti,` vs B `tvári,`; A `R.` vs B ``; A `nanájde,` vs B `nenájde,`; A `byť,` vs B `žiť,`; A `Skúsme sa častejšia pomodliť, skúsme nežne teplo pocítiť, … (40 slov)` vs B `Stále medzi nami žije Mária. Stále medzi nami, … (10 slov)`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: – · tituly: `Šťastie` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.5: `tváti,`; v2 r.1: `R.`; v3 r.5: `nanájde,`; v3 r.7: `byť,`; v4 r.1–8: `Skúsme sa častejšia pomodliť, skúsme nežne teplo pocítiť, ktoré zavanie v našich srdiečkach a z duší … (40 slov)`
- **B**: tagy: – · tituly: `Je dnes taký zvláštne krásny deň` · verseOrder `v1 v2 v3 v2` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.5: `tvári,`; v3 r.5: `nenájde,`; v3 r.7: `žiť,`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Šťastie (Mariánska).xml` (A)
- **Zmazať / zlúčiť:** `Je dnes taký zvláštne krásny deň (Mariánska).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A má 3 slohy a refrén (139 slov), B len 2 slohy a refrén (98 slov); chýba jej 3. sloha (A, v4): `Skúsme sa častejšia pomodliť, skúsme nežne teplo pocítiť, …` (40 slov).
  - B má správnejšie tvary: `na tvári,` (A: `na tváti,`, v1 r.5) a `ktoré nenájde,` (A: `ktoré nanájde,`, v3 r.5).
  - Slovná varianta: A `že s Máriou byť,` vs B `že s Máriou žiť,` (v3 r.7).
  - A má pokyn `R.` (v2 r.1) a čísla `1.`/`2.`/`3.` v riadkoch; B má `verseOrder` `v1 v2 v3 v2`, A ho nemá.
- **Čo prevziať z ostatných:**
  - V A opraviť `tváti` → `tvári`, `nanájde` → `nenájde`; rozhodnúť `byť`/`žiť`; pridať druhý titul `Je dnes taký zvláštne krásny deň`; doplniť `verseOrder` «v1 v2 v3 v2 v4 v2».
- **Istota:** stredná – Úplnosť slôh hovorí za A, preklepy A sa dajú opraviť podľa B.

**Riziká a neistoty:**

- A má v 3. sloha `častejšia`, čo môže byť ďalší preklep (neisté).

---

<a id="g40"></a>
## G40 · [4c] `Túžim priniesť na oltár (Richard Čanaky).xml` · `Obeta srdca (Obetné dary).xml` · `tuzim priniest (detsky zbor).xml`

**Zhrnutie:** A a B majú rovnaký text, C má v posledných riadkoch iné znenie; A má najlepšie delenie, B `verseOrder`.

**Súbory v skupine:**
- **A** = `Túžim priniesť na oltár (Richard Čanaky).xml`
- **B** = `Obeta srdca (Obetné dary).xml`
- **C** = `tuzim priniest (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B | C |
|---|---|---|---|
| Zodpovedá konvencii názvu | áno | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie | nie / nie |
| Tituly | `Túžim priniesť na oltár` | `Obeta srdca` | `tuzim priniest` |
| Tagy (`<author>`) | `Richard Čanaky` | `Obetné dary` | `detsky zbor` |
| songbooks | – | – | – |
| verseOrder | – | `v1 v2 v3 v2` | – |
| copyright / ccliNo | – / – | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 c1 c2 c3 v3 v4` | `v1 v2 v3` | `v1` |
| Počet slôh / `<lines>` blokov | 7 / 7 | 3 / 3 | 1 / 1 |
| Počet riadkov (neprázdnych) | 28 (28) | 19 (19) | 35 (28) |
| Počet slov (bez čísel slôh) | 117 | 118 | 119 |
| verseOrder vs dokument | – | líši sa od poradia v dokumente | – |
| Slov po rozbalení verseOrder | 117 | 167 | 119 |
| Riadky s číslom slohy na začiatku (`1.`) | 1 | 2 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 | 7 |
| Riadky s koncovou medzerou | 7 | 0 | 1 |
| Riadky s dvojitou medzerou vnútri | 0 | 1 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- B v2 r.1: `R: Povedz, čo Ti smiem dať, čo priniesť Ti smiem? Si môj láskavý Kráľ, ja len miznúci tieň.`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 117 slov v A, 118 slov v B; 1 miest s rozdielom obsahu
1. [pokyn v texte] B v2 r.1: `R:` – v A tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 8, veľkosť písmen: 4
     - interpunkcia: A v1 r.1 `oltár,` vs B v1 r.1 `oltár`; A v1 r.4 `chváliť,` vs B v1 r.4 `chváliť`; A v2 r.1 `dnes` vs B v1 r.5 `dnes,`; A c1 r.2 `smiem,` vs B v2 r.1 `smiem?`; A c1 r.4 `tieň,` vs B v2 r.1 `tieň.`; A c2 r.1 `Ježiš,` vs B v2 r.2 `Ježiš`; A c3 r.3 `dám,` vs B v2 r.3 `dám`; A v3 r.2 `sám,` vs B v3 r.2 `sám.`
     - veľkosť písmen: A v1 r.3 `tvojou` vs B v1 r.3 `Tvojou`; A c1 r.3 `si` vs B v2 r.1 `Si`; A v3 r.3 `život` vs B v3 r.3 `Život`; A v4 r.4 `tvoj.` vs B v3 r.8 `Tvoj.`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v B: `R:`×1
   - V poradí hrania (po rozbalení verseOrder): 117 vs 167 slov, 2 miest s rozdielom obsahu: A `` vs B `R:`; A `` vs B `R: Povedz, čo Ti smiem dať, čo priniesť … (49 slov)`

*Dvojica A ↔ C:* 117 slov v A, 119 slov v C; 4 miest s rozdielom obsahu
2. [iný text] A c1 r.3: `Kráľ,`  vs  C v1 r.13: `Pán,`
     - riadok v A: `si môj láskavý Kráľ,`
     - riadok v C: `Si môj láskavý Pán,`
3. [iný text] A v4 r.3: `otvoril`  vs  C v1 r.32: `Očistil`
     - riadok v A: `otvoril si bránu nebies,`
     - riadok v C: `Očistil si vnútro mne`
4. [iný text] A v4 r.3–4: `bránu nebies, dnes`  vs  C v1 r.32–33: `vnútro mne Ja viem, že`
5. [iný text] A v4 r.4: `iba`  vs  C v1 r.33: `len`
     - riadok v A: `dnes som iba tvoj.`
     - riadok v C: `Ja viem, že som len tvoj.`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 6, veľkosť písmen: 10
     - interpunkcia: A v1 r.1 `oltár,` vs C v1 r.1 `oltár`; A c1 r.2 `smiem,` vs C v1 r.12 `smiem.`; A c1 r.4 `tieň,` vs C v1 r.14 `tieň.`; A c2 r.2 `tiež,` vs C v1 r.16 `tiež.`; A v3 r.2 `sám,` vs C v1 r.26 `sám.`; A v4 r.2 `boj,` vs C v1 r.31 `boj.`
     - veľkosť písmen: A v1 r.4 `Ťa` vs C v1 r.4 `ťa`; A v2 r.1 `Ti` vs C v1 r.6 `ti`; A c1 r.1 `Ti` vs C v1 r.11 `ti`; A c1 r.2 `Ti` vs C v1 r.12 `ti`; A c1 r.3 `si` vs C v1 r.13 `Si`; A c2 r.3 `aj` vs C v1 r.17 `Aj`; A c2 r.4 `Ti` vs C v1 r.18 `ti`; A c3 r.3 `Ti` vs C v1 r.22 `ti` … (+2)
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `bránu`×1, `dnes`×1, `iba`×1, `Kráľ,`×1, `nebies,`×1, `otvoril`×1; viac v C: `ja`×1, `len`×1, `mne`×1, `Očistil`×1, `Pán.`×1, `viem,`×1, `vnútro`×1, `že`×1
   - V poradí hrania (po rozbalení verseOrder): 117 vs 119 slov, 4 miest s rozdielom obsahu: A `Kráľ,` vs C `Pán,`; A `otvoril` vs C `Očistil`; A `bránu nebies, dnes` vs C `vnútro mne Ja viem, že`; A `iba` vs C `len`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Richard Čanaky` · tituly: `Túžim priniesť na oltár` · text: nič unikátne
- **B**: tagy: `Obetné dary` · tituly: `Obeta srdca` · verseOrder `v1 v2 v3 v2` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.1: `R:`
- **C**: tagy: `detsky zbor` · tituly: `tuzim priniest` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.13: `Pán,`; v1 r.32: `Očistil`; v1 r.32–33: `vnútro mne Ja viem, že`; v1 r.33: `len`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Túžim priniesť na oltár (Richard Čanaky).xml` (A)
- **Zmazať / zlúčiť:** `Obeta srdca (Obetné dary).xml` (B), `tuzim priniest (detsky zbor).xml` (C) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A a B sa líšia len pokynom `R:` v B (v2 r.1); C sa od oboch líši na 4 miestach: `Si môj láskavý Pán,` (A, B: `Kráľ,`) a v poslednej sloha `Očistil si vnútro mne` / `Ja viem, že som len tvoj.` (A, B: `otvoril si bránu nebies,` / `dnes som iba tvoj.`).
  - A delí text na 4-riadkové slajdy (28 riadkov); B má refrén v troch dlhých riadkoch s pokynom `R:`; C je jedna 35-riadková sloha so 7 prázdnymi riadkami a titulom `tuzim priniest`.
  - B má `verseOrder` `v1 v2 v3 v2` (refrén po každej dvojici slôh); A ho nemá, takže refrén `c1`–`c3` zaznie len raz (po v2).
  - Tagy: A reálny `Richard Čanaky`, B `Obetné dary`, C `detsky zbor`.
- **Čo prevziať z ostatných:**
  - Do A doplniť `verseOrder` «v1 v2 c1 c2 c3 v3 v4 c1 c2 c3»; pridať tagy `Obetné dary`, `detsky zbor` a druhý titul `Obeta srdca`.
- **Istota:** stredná – A a B sa zhodujú v texte; C je v menšine, ale nie je overené, ktoré znenie je pôvodné.

**Riziká a neistoty:**

- Znenie C (`Očistil si vnútro mne`) môže byť iná autorská verzia; po zmazaní C sa stratí.

---

<a id="g41"></a>
## G41 · [4c] `Ty si Najvyšší, Ty si Pán (Author Unknown).xml` · `Ty si najvyssi (detsky zbor).xml`

**Zhrnutie:** Rovnaký text; B má preklepy `ponúka` a `svitim`.

Existuje aj verzia s akordmi: `Ty si najvyssi (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Ty si Najvyšší, Ty si Pán (Author Unknown).xml`
- **B** = `Ty si najvyssi (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Ty si Najvyšší, Ty si Pán` | `Ty si najvyssi` |
| Tagy (`<author>`) | `Author Unknown` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1` | `v1` |
| Počet slôh / `<lines>` blokov | 1 / 1 | 1 / 1 |
| Počet riadkov (neprázdnych) | 4 (4) | 2 (2) |
| Počet slov (bez čísel slôh) | 21 | 21 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 21 | 21 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 4 | 4 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 21 slov v A, 21 slov v B; 2 miest s rozdielom obsahu
1. [preklep / zmena slova] A v1 r.2: `ponúkam.`  vs  B v1 r.1: `ponúka.`
     - riadok v A: `to, čo mám, Tebe ponúkam. :\|`
     - riadok v B: `/: Ty si najvyšší, ty si Pán, to, čo mám, tebe ponúka. :/`
2. [preklep / zmena slova] A v1 r.4: `svietim`  vs  B v1 r.2: `svitim.`
     - riadok v A: `nech ako Ty stále svietim :\|`
     - riadok v B: `/: Obnov ma svojím Duchom Svätým, nech ako ty stále svitim. :/`
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 4
     - veľkosť písmen: A v1 r.1 `Najvyšší,` vs B v1 r.1 `najvyšší,`; A v1 r.1 `Ty` vs B v1 r.1 `ty`; A v1 r.2 `Tebe` vs B v1 r.1 `tebe`; A v1 r.4 `Ty` vs B v1 r.2 `ty`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `ponúkam.`×1, `svietim`×1; viac v B: `ponúka.`×1, `svitim.`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Author Unknown` · tituly: `Ty si Najvyšší, Ty si Pán` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.2: `ponúkam.`; v1 r.4: `svietim`
- **B**: tagy: `detsky zbor` · tituly: `Ty si najvyssi` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1: `ponúka.`; v1 r.2: `svitim.`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Ty si Najvyšší, Ty si Pán (Author Unknown).xml` (A)
- **Zmazať / zlúčiť:** `Ty si najvyssi (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - A `to, čo mám, Tebe ponúkam.` (v1 r.2) vs B `to, čo mám, tebe ponúka.` (v1 r.1).
  - A `nech ako Ty stále svietim` (v1 r.4) vs B `nech ako ty stále svitim.` (v1 r.2).
  - B zlučuje text do 2 dlhých riadkov a má titul bez diakritiky `Ty si najvyssi`; A má 4 riadky so značkami `|: … :|`.
  - A má zástupný tag `Author Unknown`, B reálny `detsky zbor`, ktorý sa prenesie.
- **Čo prevziať z ostatných:**
  - Pridať tag `detsky zbor` (a zástupný `Author Unknown` vynechať) → názov «Ty si Najvyšší, Ty si Pán (detsky zbor).xml».
- **Istota:** vysoká – Rozdiel sú dva preklepy v B.

**Riziká a neistoty:**

- Žiadne zvláštne; rozdiely sú overené skriptom.

---

<a id="g42"></a>
## G42 · [4c] `Ty si mojou láskou (detsky zbor).xml` · `Ty si mojou láskou (Anonymous).xml`

**Zhrnutie:** Rovnaký text; B má preklepy `Aleuja`, všetko v jednej 25-riadkovej sloha s `<p/>`.

**Súbory v skupine:**
- **A** = `Ty si mojou láskou (detsky zbor).xml`
- **B** = `Ty si mojou láskou (Anonymous).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Ty si mojou láskou` | `Ty si mojou láskou` |
| Tagy (`<author>`) | `detsky zbor` | `Anonymous` |
| songbooks | – | – |
| verseOrder | `v1 c1 v2 c1` | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 c1` | `v1` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 1 / 1 |
| Počet riadkov (neprázdnych) | 10 (10) | 25 (25) |
| Počet slov (bez čísel slôh) | 63 | 74 |
| verseOrder vs dokument | líši sa od poradia v dokumente | – |
| Slov po rozbalení verseOrder | 69 | 74 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 1 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 5 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 63 slov v A, 74 slov v B; 5 miest s rozdielom obsahu
1. [chýba v A] B v1 r.5: `<p/>` – v A tento text nie je
2. [chýba v A] B v1 r.10–13: `<p/> Aleuja, aleluja, aleluja tebe spievať chcem <p/>` – v A tento text nie je
3. [chýba v A] B v1 r.18: `<p/>` – v A tento text nie je
4. [chýba v A] B v1 r.23: `<p/>` – v A tento text nie je
5. [preklep / zmena slova] A c1 r.1: `aleluja,`  vs  B v1 r.24: `aleuja,`
     - riadok v A: `Aleluja, aleluja, aleluja`
     - riadok v B: `Aleluja, aleuja, aleluja`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 1
     - interpunkcia: A v1 r.3 `skrývaš` vs B v1 r.8 `skrývaš,`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v B: `Aleluja,`×1, `Aleuja,`×2, `chcem`×1, `<p/>`×5, `spievať`×1, `tebe`×1
   - V poradí hrania (po rozbalení verseOrder): 69 vs 74 slov, 6 miest s rozdielom obsahu: A `` vs B `<p/>`; A `Aleluja,` vs B `<p/> Aleuja,`; A `` vs B `<p/>`; A `` vs B `<p/>`; A `` vs B `<p/>`; A `aleluja,` vs B `aleuja,`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `detsky zbor` · tituly: – · verseOrder `v1 c1 v2 c1` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1: `aleluja,`
- **B**: tagy: `Anonymous` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.5: `<p/>`; v1 r.10–13: `<p/> Aleuja, aleluja, aleluja tebe spievať chcem <p/>`; v1 r.18: `<p/>`; v1 r.23: `<p/>`; v1 r.24: `aleuja,`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Ty si mojou láskou (detsky zbor).xml` (A)
- **Zmazať / zlúčiť:** `Ty si mojou láskou (Anonymous).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B má v refréne preklepy: `Aleuja, aleluja, aleluja` (v1 r.11) a `Aleluja, aleuja, aleluja` (v1 r.24); A má `Aleluja, aleluja, aleluja`.
  - B je jedna sloha s 5 vloženými `<p/>`; A má `v1`, `v2`, `c1` a `verseOrder` `v1 c1 v2 c1`.
  - Zvyšný text je slovo po slove rovnaký; B nemá žiadny unikátny text ani tag (A už má `detsky zbor`).
- **Čo prevziať z ostatných:** nič.
- **Istota:** vysoká – B je horšia kópia toho istého textu.

**Riziká a neistoty:**

- Žiadne zvláštne; rozdiely sú overené skriptom.

---

<a id="g43"></a>
## G43 · [4c] `Ty si Pánom, Ty si Kráľom (Prijímanie).xml` · `Ty si Pánom (...).xml` · `Ty si panom, ty si kralom (detsky zbor).xml`

**Zhrnutie:** A je úplnejšia ako B (má `Tak` a `ó aleluja`); C má unikátne ozveny `(ty si Pánom)` a `kráľa` namiesto `Pána`.

Existuje aj verzia s akordmi: `Ty si panom, ty si kralom (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Ty si Pánom, Ty si Kráľom (Prijímanie).xml`
- **B** = `Ty si Pánom (...).xml`
- **C** = `Ty si panom, ty si kralom (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B | C |
|---|---|---|---|
| Zodpovedá konvencii názvu | áno | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie | nie / nie |
| Tituly | `Ty si Pánom, Ty si Kráľom` | `Ty si Pánom` | `Ty si panom, ty si kralom` |
| Tagy (`<author>`) | `Prijímanie` | `...` | `detsky zbor` |
| songbooks | – | – | – |
| verseOrder | – | – | – |
| copyright / ccliNo | – / – | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2` | `v1 v2` | `v1` |
| Počet slôh / `<lines>` blokov | 2 / 2 | 2 / 2 | 1 / 1 |
| Počet riadkov (neprázdnych) | 6 (6) | 7 (7) | 8 (7) |
| Počet slov (bez čísel slôh) | 27 | 24 | 32 |
| verseOrder vs dokument | – | – | – |
| Slov po rozbalení verseOrder | 27 | 24 | 32 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 | 1 |
| Riadky s koncovou medzerou | 0 | 1 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 4 | 0 | 4 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF | CRLF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- C v1 r.1 (zátvorka): `(ty si Pánom)`
- C v1 r.2 (zátvorka): `(ty si kráľom)`
- C v1 r.6 (zátvorka): `( ó, aleluja)`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 27 slov v A, 24 slov v B; 2 miest s rozdielom obsahu
1. [chýba v B] A v2 r.1: `Tak` – v B tento text nie je
2. [chýba v B] A v2 r.2: `ó aleluja` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 2, veľkosť písmen: 3
     - interpunkcia: A v1 r.1 `Kráľom` vs B v1 r.2 `Kráľom,`; A v1 r.2 `Boh` vs B v1 r.3 `Boh.`
     - veľkosť písmen: A v2 r.1 `pozdvihnime` vs B v2 r.1 `Pozdvihnime`; A v2 r.4 `Velebme` vs B v2 r.4 `velebme`; A v2 r.4 `ho` vs B v2 r.4 `Ho.`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `aleluja`×1, `ó,`×1, `Tak`×1; viac v B: –

*Dvojica A ↔ C:* 27 slov v A, 32 slov v C; 3 miest s rozdielom obsahu
3. [chýba v A] C v1 r.1–2: `(ty si Pánom) ty si kráľom,` – v A tento text nie je
4. [chýba v C] A v2 r.1: `Tak` – v C tento text nie je
5. [iný text] A v2 r.3: `Pána`  vs  C v1 r.7: `kráľa`
     - riadok v A: `postavme sa pred tvár Pána`
     - riadok v C: `postavme sa pred tvár kráľa`
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 5, interpunkcia: 4
     - veľkosť písmen: A v1 r.1 `Ty` vs C v1 r.2 `(ty`; A v1 r.1 `Kráľom` vs C v1 r.2 `kráľom)`; A v1 r.2 `Kráľom` vs C v1 r.3 `kráľom`; A v2 r.1 `pozdvihnime` vs C v1 r.5 `Pozdvihnime`; A v2 r.4 `Velebme` vs C v1 r.8 `velebme`
     - interpunkcia: A v1 r.2 `Boh` vs C v1 r.3 `Boh.:/`; A v2 r.2 `ó` vs C v1 r.6 `ó,`; A v2 r.2 `aleluja` vs C v1 r.6 `aleluja)`; A v2 r.4 `ho` vs C v1 r.8 `ho.:/`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `Pána`×1, `Tak`×1; viac v C: `kráľa`×1, `Kráľom`×1, `Pánom,`×1, `si`×2, `Ty`×2

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Prijímanie` · tituly: `Ty si Pánom, Ty si Kráľom` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.1: `Tak`
- **B**: tagy: `...` · tituly: `Ty si Pánom` · text: nič unikátne
- **C**: tagy: `detsky zbor` · tituly: `Ty si panom, ty si kralom` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1–2: `(ty si Pánom) ty si kráľom,`; v1 r.7: `kráľa`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Ty si Pánom, Ty si Kráľom (Prijímanie).xml` (A)
- **Zmazať / zlúčiť:** `Ty si Pánom (...).xml` (B), `Ty si panom, ty si kralom (detsky zbor).xml` (C) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B nemá slová `Tak` a `ó aleluja` (A, v2 r.1–2: `Tak pozdvihnime svoje srdcia,` / `pozdvihnime svoje dlane, ó aleluja`) a má 24 slov oproti 27 v A.
  - C má unikátne ozveny v zátvorkách: `/: Ty si Pánom, (ty si Pánom)`, `ty si kráľom, (ty si kráľom)` a `( ó, aleluja)`, ktoré sa zobrazia na slajde; A ich nemá.
  - C má `postavme sa pred tvár kráľa` (A, B: `tvár Pána`) a nemá `Tak`.
  - A má reálny tag `Prijímanie`, B zástupný `...`, C `detsky zbor`; C je jedna 8-riadková sloha s titulom bez diakritiky.
- **Čo prevziať z ostatných:**
  - Pridať tag `detsky zbor`; rozhodnúť, či sa ozveny z C (`(ty si Pánom)`, `(ty si kráľom)`) majú zapísať aj do A.
- **Istota:** stredná – A je nadmnožina B; unikátne ozveny v C sú otvorená otázka.

**Riziká a neistoty:**

- Zmazaním C sa stratia ozveny v zátvorkách.

---

<a id="g44"></a>
## G44 · [4c] `Vládca (MaranaTha).xml` · `Vladca (detsky zbor).xml`

**Zhrnutie:** Rovnaké slová (86 : 86); B má `verseOrder` a refrén `c1`/mostík `c2`, A má reálny tag a dva tituly.

**Súbory v skupine:**
- **A** = `Vládca (MaranaTha).xml`
- **B** = `Vladca (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Vládca`<br>`Každý z nás dúfa v súcit` | `Vladca` |
| Tagy (`<author>`) | `MaranaTha` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | `v1 c1 v2 c1 c2 c1` |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 c1 v2 b1` | `v1 v2 c1 c2` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 4 / 4 |
| Počet riadkov (neprázdnych) | 24 (22) | 12 (12) |
| Počet slov (bez čísel slôh) | 86 | 86 |
| verseOrder vs dokument | – | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 86 | 134 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 2 | 0 |
| Riadky s koncovou medzerou | 1 | 0 |
| Riadky s dvojitou medzerou vnútri | 1 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 2 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 86 slov v A, 86 slov v B; 1 miest s rozdielom obsahu
1. [rovnaký text na inom mieste (iné poradie slôh)] A c1 r.1–6 a B c1 r.1–4: `Vládca, vrchmi môže hýbať Môj Boh je najmocnejší má moc … (24 slov)`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 13, veľkosť písmen: 5, značky opakovania: 1
     - interpunkcia: A v1 r.2 `lásku` vs B v1 r.1 `lásku,`; A v1 r.3 `sa` vs B v1 r.2 `sa.`; A v1 r.6 `spásy` vs B v1 r.3 `spásy.`; A v2 r.1 `prijímaš` vs B v2 r.1 `prijímaš,`; A v2 r.2 `pády` vs B v2 r.1 `pády,`; A v2 r.3 `sa` vs B v2 r.2 `sa.`; A v2 r.4 `kráčať` vs B v2 r.2 `kráčať,`; A v2 r.5 `nádej` vs B v2 r.3 `nádej,` … (+5)
     - veľkosť písmen: A v2 r.1 `ty` vs B v2 r.1 `Ty`; A v2 r.4 `tebou` vs B v2 r.2 `Tebou`; A v2 r.6 `ti` vs B v2 r.3 `Ti`; A b1 r.2 `ťa` vs B c2 r.1 `Ťa`; A b1 r.4 `kráľ` vs B c2 r.2 `Kráľ`
     - značky opakovania: A b1 r.1 `Zažiar` vs B c2 r.1 `/:Zažiar`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v B: –
   - V poradí hrania (po rozbalení verseOrder): 86 vs 134 slov, 2 miest s rozdielom obsahu: A `` vs B `Vládca, vrchmi môže hýbať, môj Boh je najmocnejší, … (24 slov)`; A `` vs B `Vládca, vrchmi môže hýbať, môj Boh je najmocnejší, … (24 slov)`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `MaranaTha` · tituly: `Každý z nás dúfa v súcit`, `Vládca` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1–6: `Vládca, vrchmi môže hýbať Môj Boh je najmocnejší má moc zachrániť nás Víťaz, pôvod večnej spásy … (24 slov)`
- **B**: tagy: `detsky zbor` · tituly: `Vladca` · verseOrder `v1 c1 v2 c1 c2 c1` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1–4: `Vládca, vrchmi môže hýbať, môj Boh je najmocnejší, má moc zachrániť nás. Víťaz, pôvod večnej spásy, … (24 slov)`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Vládca (MaranaTha).xml` (A)
- **Zmazať / zlúčiť:** `Vladca (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Obsah je slovo po slove rovnaký, rozdiel je len delenie: A má `v1`, `c1`, `v2`, `b1` s kratšími riadkami; B `v1`, `v2`, `c1`, `c2` s dlhšími riadkami.
  - B má `verseOrder` `v1 c1 v2 c1 c2 c1` (refrén po každej sloha); A nemá `verseOrder`, refrén `c1` zaznie raz.
  - A má dva tituly (`Vládca`, `Každý z nás dúfa v súcit`) a reálny tag `MaranaTha`; B titul bez diakritiky `Vladca` a tag `detsky zbor`.
  - A má v refréne neprirodzené zalomenie `hýbať Môj Boh je najmocnejší` (c1 r.1–2) a dva prázdne riadky; B delí riadky pri vete.
- **Čo prevziať z ostatných:**
  - Do A doplniť `verseOrder` «v1 c1 v2 c1 b1 c1» (podľa B) a tag `detsky zbor`.
- **Istota:** vysoká – Obsah je totožný; rozdiel je len štruktúra, ktorú sa dá preniesť.

**Riziká a neistoty:**

- Prirodzené zalomenie riadkov v refréne A je vecou úpravy po zlúčení.

---

<a id="g45"></a>
## G45 · [4c] `Všade tam kde sú (detsky zbor).xml` · `Všade tam kde sú (Anonymous).xml` · `Privítajme Pána (Začiatok).xml`

**Zhrnutie:** Rovnaký text; B má zlepené slová (`Ježišv`, `ženáš`, `Pánav`), C pokyn `R:` a nezlomiteľné medzery; A je čistá.

Existuje aj verzia s akordmi: `Všade tam kde sú (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Všade tam kde sú (detsky zbor).xml`
- **B** = `Všade tam kde sú (Anonymous).xml`
- **C** = `Privítajme Pána (Začiatok).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B | C |
|---|---|---|---|
| Zodpovedá konvencii názvu | áno | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie | áno / áno |
| Tituly | `Všade tam kde sú` | `Všade tam kde sú` | `Privítajme Pána` |
| Tagy (`<author>`) | `detsky zbor` | `Anonymous` | `Začiatok` |
| songbooks | – | – | – |
| verseOrder | `v1 c1` | – | – |
| copyright / ccliNo | – / – | – / – | – / – |
| Slohy v poradí dokumentu | `v1 c1` | `v1 c1` | `v1 v2` |
| Počet slôh / `<lines>` blokov | 2 / 2 | 2 / 2 | 2 / 2 |
| Počet riadkov (neprázdnych) | 7 (7) | 10 (10) | 10 (10) |
| Počet slov (bez čísel slôh) | 46 | 42 | 47 |
| verseOrder vs dokument | zhoduje sa s dokumentom | – | – |
| Slov po rozbalení verseOrder | 46 | 42 | 47 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 2 | 2 | 2 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- C v2 r.1: `R: \|: Privítajme Pána v tomto chráme,`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 46 slov v A, 42 slov v B; 4 miest s rozdielom obsahu
1. [preklep / zmena slova] A v1 r.1: `tam, kde`  vs  B v1 r.1: `tam,kde`
     - riadok v A: `Všade tam, kde sú ľudia zídení`
     - riadok v B: `Všade tam,kde sú ľudia zídení`
2. [preklep / zmena slova] A v1 r.2: `Ježiš, v`  vs  B v1 r.2: `Ježišv`
     - riadok v A: `v mene Ježiš, v láske zjednotení.`
     - riadok v B: `v mene Ježišv láske zjednotení.`
3. [preklep / zmena slova] A v1 r.4: `že náš`  vs  B v1 r.5: `ženáš`
     - riadok v A: `dnes viem, že náš Boh je na tomto mieste prítomný.`
     - riadok v B: `Dnes viem, ženáš Boh je`
4. [preklep / zmena slova] A c1 r.1: `Pána v`  vs  B c1 r.1: `Pánav`
     - riadok v A: `/:Privítajme Pána v tomto chráme,`
     - riadok v B: `/: Privítajme Pánav tomto chráme,`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 1, veľkosť písmen: 1, značky opakovania: 2
     - interpunkcia: A v1 r.3 `prítomný,` vs B v1 r.4 `prítomný.`
     - veľkosť písmen: A v1 r.4 `dnes` vs B v1 r.5 `Dnes`
     - značky opakovania: A c1 r.1 `/:Privítajme` vs B c1 r.1 `Privítajme`; A c1 r.3 `spasených.:/` vs B c1 r.4 `spasených.`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `Ježiš,`×1, `kde`×1, `náš`×1, `Pána`×1, `tam,`×1, `v`×2, `že`×1; viac v B: `Ježišv`×1, `Pánav`×1, `tam,kde`×1, `ženáš`×1
   - V poradí hrania (po rozbalení verseOrder): 46 vs 42 slov, 4 miest s rozdielom obsahu: A `tam, kde` vs B `tam,kde`; A `Ježiš, v` vs B `Ježišv`; A `že náš` vs B `ženáš`; A `Pána v` vs B `Pánav`

*Dvojica A ↔ C:* 46 slov v A, 47 slov v C; 1 miest s rozdielom obsahu
5. [pokyn v texte] C v2 r.1: `R:` – v A tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 5, veľkosť písmen: 2, značky opakovania: 1
     - interpunkcia: A v1 r.1 `sú` vs C v1 r.1 `sú,`; A v1 r.1 `zídení` vs C v1 r.1 `zídení,`; A v1 r.3 `prítomný,` vs C v1 r.4 `prítomný.`; A c1 r.2 `naplní.` vs C v2 r.2 `naplní,`; A c1 r.3 `spasených.:/` vs C v2 r.4 `spasených`
     - veľkosť písmen: A v1 r.4 `dnes` vs C v1 r.5 `Dnes`; A c1 r.3 `Svojmu` vs C v2 r.3 `svojmu`
     - značky opakovania: A c1 r.1 `/:Privítajme` vs C v2 r.1 `Privítajme`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v C: `R:`×1
   - V poradí hrania (po rozbalení verseOrder): 46 vs 47 slov, 1 miest s rozdielom obsahu: A `` vs C `R:`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `detsky zbor` · tituly: – · verseOrder `v1 c1` · text: nič unikátne
- **B**: tagy: `Anonymous` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1: `tam,kde`; v1 r.2: `Ježišv`; v1 r.5: `ženáš`; c1 r.1: `Pánav`
- **C**: tagy: `Začiatok` · tituly: `Privítajme Pána` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.1: `R:`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Všade tam kde sú (detsky zbor).xml` (A)
- **Zmazať / zlúčiť:** `Všade tam kde sú (Anonymous).xml` (B), `Privítajme Pána (Začiatok).xml` (C) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B má 4 zlepené/zle oddelené miesta: `tam,kde`, `Ježišv láske`, `ženáš Boh`, `Pánav tomto`; A má `tam, kde`, `Ježiš, v`, `že náš`, `Pána v`.
  - C má pokyn `R: |: Privítajme Pána v tomto chráme,` (v2 r.1), ktorý sa zobrazí na slajde, a nezlomiteľné medzery v titule aj v názve súboru.
  - A má `verseOrder` `v1 c1` a čisté značky `/:Privítajme Pána v tomto chráme,` … `pieseň spasených.:/`.
  - Tagy: A `detsky zbor`, B zástupný `Anonymous`, C reálny `Začiatok`; C má iný titul `Privítajme Pána`.
- **Čo prevziať z ostatných:**
  - Pridať tag `Začiatok` a druhý titul `Privítajme Pána` (z C); `Anonymous` vynechať → názov «Všade tam kde sú (Začiatok, detsky zbor).xml».
- **Istota:** vysoká – A má správny text; B a C pridávajú len chyby alebo pokyny.

**Riziká a neistoty:**

- Žiadne zvláštne; rozdiely sú overené skriptom.

---

<a id="g46"></a>
## G46 · [4c] `Vždy je s nami tá (Mariánska).xml` · `Vždy je s nami tá (Anonymous).xml`

**Zhrnutie:** Rovnaký text; A má `verseOrder` a refrén po 2. sloha, B pridáva refrén iba raz; rozdiel je pokyn `R:` a `Kráľovná-á`.

**Súbory v skupine:**
- **A** = `Vždy je s nami tá (Mariánska).xml`
- **B** = `Vždy je s nami tá (Anonymous).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Vždy je s nami tá` | `Vždy je s nami tá` |
| Tagy (`<author>`) | `Mariánska` | `Anonymous` |
| songbooks | – | – |
| verseOrder | `v1 v2 v3 v2` | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3` | `v1 v2 c1 v3 v4` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 5 / 5 |
| Počet riadkov (neprázdnych) | 14 (14) | 18 (18) |
| Počet slov (bez čísel slôh) | 79 | 78 |
| verseOrder vs dokument | líši sa od poradia v dokumente | – |
| Slov po rozbalení verseOrder | 109 | 78 |
| Riadky s číslom slohy na začiatku (`1.`) | 2 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 3 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- A v2 r.1: `R: Ty nás vítaš v chráme plnom lásky,`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 79 slov v A, 78 slov v B; 2 miest s rozdielom obsahu
1. [pokyn v texte] A v2 r.1: `R:` – v B tento text nie je
2. [preklep / zmena slova] A v2 r.5: `Kráľovná-á,`  vs  B c1 r.5: `kráľovná,`
     - riadok v A: `Mária, Ty naša Kráľovná-á,`
     - riadok v B: `Mária, Ty naša kráľovná,`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 4, veľkosť písmen: 4
     - interpunkcia: A v1 r.1 `ľúbi` vs B v1 r.2 `ľúbi,`; A v1 r.3 `chráni` vs B v2 r.2 `chráni,`; A v2 r.4 `silu,` vs B c1 r.4 `silu!`; A v3 r.2 `otvorí,` vs B v3 r.2 `otvorí.`
     - veľkosť písmen: A v2 r.2 `Tvojom` vs B c1 r.2 `tvojom`; A v2 r.4 `prosíme` vs B c1 r.4 `Prosíme`; A v2 r.6 `Kráľovná.` vs B c1 r.6 `kráľovná!`; A v3 r.3 `silu` vs B v4 r.1 `Silu`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `Kráľovná-á,`×1, `R:`×1; viac v B: `Kráľovná.`×1
   - V poradí hrania (po rozbalení verseOrder): 109 vs 78 slov, 3 miest s rozdielom obsahu: A `R:` vs B ``; A `Kráľovná-á,` vs B `kráľovná,`; A `R: Ty nás vítaš v chráme plnom lásky, … (30 slov)` vs B ``

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Mariánska` · tituly: – · verseOrder `v1 v2 v3 v2` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.1: `R:`; v2 r.5: `Kráľovná-á,`
- **B**: tagy: `Anonymous` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.5: `kráľovná,`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Vždy je s nami tá (Mariánska).xml` (A)
- **Zmazať / zlúčiť:** `Vždy je s nami tá (Anonymous).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Slovný rozdiel je len pokyn `R:` (A, v2 r.1: `R: Ty nás vítaš v chráme plnom lásky,`) a natiahnuté `Kráľovná-á,` (A, v2 r.5) oproti `kráľovná,` (B, c1 r.5).
  - A má `verseOrder` `v1 v2 v3 v2` (refrén po 1. aj po 2. sloha, 109 slov po rozbalení); B nemá `verseOrder`, takže refrén zaznie raz (78 slov).
  - B delí 1. a 2. sloha na 4 krátke slohy (`v1`, `v2`, `v3`, `v4`) a má 3 riadky s koncovou medzerou.
  - Tagy: A reálny `Mariánska`, B zástupný `Anonymous`.
- **Čo prevziať z ostatných:**
  - V A odstrániť pokyn `R:` (a voliteľne `-á` v `Kráľovná-á`).
- **Istota:** vysoká – B je horšia verzia toho istého textu.

**Riziká a neistoty:**

- Žiadne zvláštne; rozdiely sú overené skriptom.

---

<a id="g47"></a>
## G47 · [4c] `ZÁCHRANÁR (Večeradlo s Pannou Máriou).xml` · `Zachranar (detsky zbor).xml`

**Zhrnutie:** Rovnaké slohy; B má `verseOrder` s refrénom po každej sloha a rozpísaný refrén, A ho má raz bez `verseOrder`.

**Súbory v skupine:**
- **A** = `ZÁCHRANÁR (Večeradlo s Pannou Máriou).xml`
- **B** = `Zachranar (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `ZÁCHRANÁR` | `Zachranar` |
| Tagy (`<author>`) | `Večeradlo s Pannou Máriou` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | `v1 c1 v2 c1 v3 c1` |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 c1 v2 v3` | `v1 v2 v3 c1` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 4 / 4 |
| Počet riadkov (neprázdnych) | 14 (14) | 15 (14) |
| Počet slov (bez čísel slôh) | 72 | 75 |
| verseOrder vs dokument | – | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 72 | 93 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 1 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 4 | 4 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica B ↔ A:* 75 slov v B, 72 slov v A; 2 miest s rozdielom obsahu
1. [chýba v B] A c1 r.1–2: `[:ALELUJA,ALELUJA, ALELU:] [:Ale Ale Ale Alelujaaa:]` – v B tento text nie je
2. [chýba v A] B c1 r.1–3: `/:ALELUJA,ALELUJA, ALELU. ALELUJA, A ALELU:/ /:Ale Ale Ale Alelujaaa:/` – v A tento text nie je
   - Žiadne rozdiely v zápise (diakritika / veľkosť / interpunkcia) pri zhodných slovách.
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v B: `A`×1, `ALELU.`×1, `ALELUJA,`×1; viac v A: –
   - V poradí hrania (po rozbalení verseOrder): 93 vs 72 slov, 3 miest s rozdielom obsahu: B `ALELUJA, A ALELU:/` vs A ``; B `/:ALELUJA,ALELUJA, ALELU. ALELUJA, A ALELU:/ /:Ale Ale Ale … (9 slov)` vs A ``; B `/:ALELUJA,ALELUJA, ALELU. ALELUJA, A ALELU:/ /:Ale Ale Ale … (9 slov)` vs A ``

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Večeradlo s Pannou Máriou` · tituly: `ZÁCHRANÁR` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1–2: `[:ALELUJA,ALELUJA, ALELU:] [:Ale Ale Ale Alelujaaa:]`
- **B**: tagy: `detsky zbor` · tituly: `Zachranar` · verseOrder `v1 c1 v2 c1 v3 c1` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1–3: `/:ALELUJA,ALELUJA, ALELU. ALELUJA, A ALELU:/ /:Ale Ale Ale Alelujaaa:/`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Zachranar (detsky zbor).xml` (B)
- **Zmazať / zlúčiť:** `ZÁCHRANÁR (Večeradlo s Pannou Máriou).xml` (A) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Slohy v1–v3 sú slovo po slove rovnaké v oboch.
  - B má `verseOrder` `v1 c1 v2 c1 v3 c1` (refrén po každej sloha); A nemá `verseOrder`, refrén `c1` zaznie raz (po v1).
  - Refrén sa líši: A `[:ALELUJA,ALELUJA, ALELU:]`, B `/:ALELUJA,ALELUJA, ALELU. ALELUJA, A ALELU:/` (3 slová navyše: `ALELUJA, A ALELU`).
  - A má titul veľkými písmenami `ZÁCHRANÁR` a reálny tag `Večeradlo s Pannou Máriou`; B titul bez diakritiky `Zachranar` a tag `detsky zbor`.
- **Čo prevziať z ostatných:**
  - Do B pridať tag `Večeradlo s Pannou Máriou` a titul «Záchranár».
- **Istota:** stredná – Štruktúra hovorí za B, ale nie je jasné, ktoré znenie refrénu je správne.

**Riziká a neistoty:**

- Dlhšie znenie refrénu v B (`ALELUJA, A ALELU`) nie je overené.

---

<a id="g48"></a>
## G48 · [4c] `Zvelebený Pán (Rieka Života).xml` · `Zvelebený buď (detsky zbor).xml`

**Zhrnutie:** Rovnaký text až na dve slová (`pustinách`/`pustatinách`, `púti`/`púšti`); B má všetky slohy zlepené do 3 dlhých riadkov s číslami a pokynmi.

**Súbory v skupine:**
- **A** = `Zvelebený Pán (Rieka Života).xml`
- **B** = `Zvelebený buď (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Zvelebený Pán` | `Zvelebený buď` |
| Tagy (`<author>`) | `Rieka Života` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 c1 c2 v3 v4 e1` | `v1a v1b v1c e1` |
| Počet slôh / `<lines>` blokov | 7 / 7 | 4 / 4 |
| Počet riadkov (neprázdnych) | 28 (28) | 5 (5) |
| Počet slov (bez čísel slôh) | 104 | 105 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 104 | 105 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 1 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 1 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 1 | 1 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 104 slov v A, 105 slov v B; 3 miest s rozdielom obsahu
1. [preklep / zmena slova] A v2 r.3: `pustinách`  vs  B v1a r.1: `pustatinách,`
     - riadok v A: `aj keď kráčam sám v pustinách`
     - riadok v B: `1.Zvelebený buď tam, kde kraj medom oplýva, tam, kde rieky vždy hojné sú, zvelebený Pán. Zvelebený buď, aj keď v púšti sa nachádzam, aj keď kráčam sám v pustatinách, zvelebený Pán.`
2. [pokyn v texte] B v1b r.1: `R.` – v A tento text nie je
3. [preklep / zmena slova] A v4 r.2: `púti,`  vs  B v1c r.1: `púšti,`
     - riadok v A: `aj na púti, čo ťažká je`
     - riadok v B: `2. Zvelebený buď, keď ma lúč slnka zohrieva, keď je svet krásny bez tieňa, zvelebený Pán. Zvelebený buď aj na púšti, čo ťažká je, aj keď obetu prinášam, zvelebený Pán.`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 25, veľkosť písmen: 1
     - interpunkcia: A v1 r.2 `oplýva` vs B v1a r.1 `oplýva,`; A v1 r.3 `sú` vs B v1a r.1 `sú,`; A v1 r.4 `Pán` vs B v1a r.1 `Pán.`; A v2 r.1 `buď` vs B v1a r.1 `buď,`; A v2 r.2 `nachádzam` vs B v1a r.1 `nachádzam,`; A v2 r.4 `Pán` vs B v1a r.1 `Pán.`; A c1 r.1 `dávaš` vs B v1b r.1 `dávaš,`; A c1 r.2 `rád` vs B v1b r.1 `rád,` … (+17)
     - veľkosť písmen: A e1 r.2 `Máš` vs B e1 r.1 `máš`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `pustinách`×1, `púti,`×1; viac v B: `pustatinách,`×1, `púšti`×1, `R.`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Rieka Života` · tituly: `Zvelebený Pán` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.3: `pustinách`; v4 r.2: `púti,`
- **B**: tagy: `detsky zbor` · tituly: `Zvelebený buď` · text (slová, ktoré v žiadnom inom súbore nie sú): v1a r.1: `pustatinách,`; v1b r.1: `R.`; v1c r.1: `púšti,`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Zvelebený Pán (Rieka Života).xml` (A)
- **Zmazať / zlúčiť:** `Zvelebený buď (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B má slohy v 3 riadkoch po 29–31 slov, s číslami zlepenými s textom: `1.Zvelebený buď tam, kde kraj medom oplýva, …`, `R. Každú milosť, čo mi dávaš, …`, `2. Zvelebený buď, keď ma lúč slnka zohrieva, …`; A má 7 slôh po 4 riadkoch.
  - Slová: A `aj keď kráčam sám v pustinách` (v2 r.3) vs B `aj keď kráčam sám v pustatinách,`; A `aj na púti, čo ťažká je` (v4 r.2) vs B `aj na púšti, čo ťažká je`.
  - B nemá žiadny unikátny text okrem týchto variantov a pokynu `R.`; tag A je reálny `Rieka Života`.
- **Čo prevziať z ostatných:**
  - Pridať tag `detsky zbor` a druhý titul `Zvelebený buď`; rozhodnúť `pustinách`/`pustatinách` a `púti`/`púšti`.
- **Istota:** stredná – Štruktúra je jasná, dve slová sú neisté.

**Riziká a neistoty:**

- `púšti` v B sa opakuje s 1. slohou (`aj keď v púšti sa nachádzam`), preto môže byť A pôvodnejšia (neisté).

---

<a id="g49"></a>
## G49 · [4c] `Žalm 131 (Anonymous).xml` · `Nasytene dieta - Zalm 131 (detsky zbor).xml`

**Zhrnutie:** Rovnaké slová (48 : 48); B má `verseOrder` s refrénom pred, medzi a po slohách; titul B treba opraviť.

Existuje aj verzia s akordmi: `Nasytene dieta - Zalm 131 (MlaKa, akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Žalm 131 (Anonymous).xml`
- **B** = `Nasytene dieta - Zalm 131 (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Žalm 131` | `Nasytene dieta - Zalm 131` |
| Tagy (`<author>`) | `Anonymous` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | `c1 v1 c1 v2 c1` |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 c1 v2` | `v1 v2 c1` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 3 / 3 |
| Počet riadkov (neprázdnych) | 8 (8) | 10 (10) |
| Počet slov (bez čísel slôh) | 48 | 48 |
| verseOrder vs dokument | – | líši sa od poradia v dokumente |
| Slov po rozbalení verseOrder | 48 | 78 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 2 | 2 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica B ↔ A:* 48 slov v B, 48 slov v A; 1 miest s rozdielom obsahu
1. [rovnaký text na inom mieste (iné poradie slôh)] B c1 r.1–2 a A c1 r.1–2: `Ako nasýtené dieťa v matkinom náručí. Ako nasýtené dieťa tak … (15 slov)`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 6
     - interpunkcia: B v1 r.1 `Pane,` vs A v1 r.1 `Pane`; B v1 r.1 `nevystatuje.` vs A v1 r.1 `nevystatuje`; B v1 r.4 `nedosiahnuteľnými.` vs A v1 r.4 `nedosiahnuteľnými`; B v2 r.2 `utíšil.` vs A v2 r.1 `utíšil`; B v2 r.3 `Dúfaj,` vs A v2 r.2 `Dúfaj`; B v2 r.3 `Izrael,` vs A v2 r.2 `Izrael`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v B: –; viac v A: –
   - V poradí hrania (po rozbalení verseOrder): 78 vs 48 slov, 2 miest s rozdielom obsahu: B `Ako nasýtené dieťa v matkinom náručí. Ako nasýtené … (15 slov)` vs A ``; B `Ako nasýtené dieťa v matkinom náručí. Ako nasýtené … (15 slov)` vs A ``

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Anonymous` · tituly: `Žalm 131` · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.1–2: `Ale ja som svoju dušu upokojil a utíšil Dúfaj Izrael v Pána odteraz až naveky.`
- **B**: tagy: `detsky zbor` · tituly: `Nasytene dieta - Zalm 131` · verseOrder `c1 v1 c1 v2 c1` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1–2: `Ako nasýtené dieťa v matkinom náručí. Ako nasýtené dieťa tak je moja duša vo mne.:/`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Nasytene dieta - Zalm 131 (detsky zbor).xml` (B)
- **Zmazať / zlúčiť:** `Žalm 131 (Anonymous).xml` (A) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Obsah je rovnaký; A má poradie `v1 c1 v2` bez `verseOrder` (refrén raz medzi slohami), B `verseOrder` `c1 v1 c1 v2 c1` (po rozbalení 78 slov).
  - B má lepšiu interpunkciu a delenie riadkov: `Pane, moje srdce sa nevystatuje.` (A: `Pane moje srdce sa nevystatuje`) a `Ale ja som svoju dušu upokojil` / `a utíšil.` (A: jeden riadok).
  - B má titul bez diakritiky `Nasytene dieta - Zalm 131`; A má `Žalm 131`.
  - A má zástupný tag `Anonymous`, takže sa nič nestratí.
- **Čo prevziať z ostatných:**
  - Opraviť titul B na «Nasýtené dieťa - Žalm 131» a pridať druhý titul `Žalm 131`.
- **Istota:** stredná – Obsah je totožný; poradie hrania v B (`c1 v1 c1 v2 c1`) nie je overené.

**Riziká a neistoty:**

- Ak sa refrén pred 1. slohou nemá hrať, upraviť `verseOrder`.

---

<a id="g50"></a>
## G50 · [4c] `ŽALM (Večeradlo s Pannou Máriou).xml` · `spievaj panovi (detsky zbor).xml`

**Zhrnutie:** Rovnaký text; B má pokyny `R:` na koncoch riadkov a nemá `verseOrder`.

Existuje aj verzia s akordmi: `spievaj panovi (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `ŽALM (Večeradlo s Pannou Máriou).xml`
- **B** = `spievaj panovi (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `ŽALM` | `spievaj panovi` |
| Tagy (`<author>`) | `Večeradlo s Pannou Máriou` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | `c1 v1 c1 v2 c1 v3 c1` | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `c1 v1 v2 v3` | `v1 v2 v3 c1` |
| Počet slôh / `<lines>` blokov | 4 / 4 | 4 / 4 |
| Počet riadkov (neprázdnych) | 15 (15) | 15 (15) |
| Počet slov (bez čísel slôh) | 66 | 70 |
| verseOrder vs dokument | líši sa od poradia v dokumente | – |
| Slov po rozbalení verseOrder | 99 | 70 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 2 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** 
- B v1 r.4: `a jeho svätého ramena. R:`
- B v2 r.4: `a na svoju vernosť voči Izraelovi. R:`
- B v3 r.4: `plesajte, radujte sa a hrajte. R:`
- B c1 r.1: `R: /: Spievaj Pánovi, spievaj Pánovi`

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 66 slov v A, 70 slov v B; 3 miest s rozdielom obsahu
1. [rovnaký text na inom mieste (iné poradie slôh)] A c1 r.1–3 a B v3 r.4 – c1 r.3: `Spievaj Pánovi, spievaj Pánovi Pieseň novú, aleluja Vykonal veci zázračné, … (11 slov)`
     - v presunutom úseku: A `` vs B `R: R:`
2. [pokyn v texte] B v1 r.4: `R:` – v A tento text nie je
3. [pokyn v texte] B v2 r.4: `R:` – v A tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 5, veľkosť písmen: 1
     - interpunkcia: A v1 r.2 `zázračné.` vs B v1 r.2 `zázračné,`; A v2 r.4 `Izraelovi` vs B v2 r.4 `Izraelovi.`; A v3 r.2 `Boha,` vs B v3 r.2 `Boha.`; A v3 r.3 `jasaj` vs B v3 r.3 `jasaj,`; A v3 r.3 `zem,` vs B v3 r.3 `zem;`
     - veľkosť písmen: A v1 r.3 `Víťazstvo` vs B v1 r.3 `víťazstvo`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v B: `R:`×4
   - V poradí hrania (po rozbalení verseOrder): 99 vs 70 slov, 4 miest s rozdielom obsahu: A `Spievaj Pánovi, spievaj Pánovi Pieseň novú, aleluja Vykonal … (11 slov)` vs B ``; A `Spievaj Pánovi, spievaj Pánovi Pieseň novú, aleluja Vykonal … (11 slov)` vs B `R:`; A `Spievaj Pánovi, spievaj Pánovi Pieseň novú, aleluja Vykonal … (11 slov)` vs B `R:`; A `` vs B `R: R:`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Večeradlo s Pannou Máriou` · tituly: `ŽALM` · verseOrder `c1 v1 c1 v2 c1 v3 c1` · text (slová, ktoré v žiadnom inom súbore nie sú): c1 r.1–3: `Spievaj Pánovi, spievaj Pánovi Pieseň novú, aleluja Vykonal veci zázračné, aleluja`
- **B**: tagy: `detsky zbor` · tituly: `spievaj panovi` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.4: `R:`; v2 r.4: `R:`; v3 r.4 – c1 r.3: `R: R: Spievaj Pánovi, spievaj Pánovi pieseň novú, aleluja, vykonal veci zázračné, aleluja.`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `ŽALM (Večeradlo s Pannou Máriou).xml` (A)
- **Zmazať / zlúčiť:** `spievaj panovi (detsky zbor).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B má v texte pokyny `a jeho svätého ramena. R:` (v1 r.4), `a na svoju vernosť voči Izraelovi. R:` (v2 r.4), `plesajte, radujte sa a hrajte. R:` (v3 r.4) a `R: /: Spievaj Pánovi, spievaj Pánovi` (c1 r.1), ktoré sa zobrazia na slajde.
  - A má `verseOrder` `c1 v1 c1 v2 c1 v3 c1` (99 slov po rozbalení); B nemá `verseOrder` (70 slov), refrén je v B posledná sloha.
  - A má titul `ŽALM` a tag `Večeradlo s Pannou Máriou`; B titul bez diakritiky `spievaj panovi` a tag `detsky zbor`.
- **Čo prevziať z ostatných:**
  - Pridať tag `detsky zbor` a druhý titul «Spievaj Pánovi».
- **Istota:** vysoká – Rozdiel sú len pokyny a chýbajúci `verseOrder` v B.

**Riziká a neistoty:**

- Žiadne zvláštne; rozdiely sú overené skriptom.

---

<a id="g51"></a>
## G51 · [4d] `Pane, zmiluj sa nad nami (Kyrie).xml` · `Pane zmiluj sa nad nami (Anonymous).xml`

**Zhrnutie:** B má 3 vzývania (Pane–Kriste–Pane), A len 2; môže ísť o rôzne nápevy Kyrie.

**Súbory v skupine:**
- **A** = `Pane, zmiluj sa nad nami (Kyrie).xml`
- **B** = `Pane zmiluj sa nad nami (Anonymous).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Pane, zmiluj sa nad nami` | `Pane zmiluj sa nad nami` |
| Tagy (`<author>`) | `Kyrie` | `Anonymous` |
| songbooks | – | – |
| verseOrder | `v1` | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1` | `v1` |
| Počet slôh / `<lines>` blokov | 1 / 1 | 1 / 1 |
| Počet riadkov (neprázdnych) | 3 (3) | 4 (4) |
| Počet slov (bez čísel slôh) | 12 | 17 |
| verseOrder vs dokument | zhoduje sa s dokumentom | – |
| Slov po rozbalení verseOrder | 12 | 17 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 12 slov v A, 17 slov v B; 1 miest s rozdielom obsahu
1. [chýba v A] B v1 r.3: `Pane, zmiluj sa nad nami.` – v A tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 4
     - interpunkcia: A v1 r.1 `nami` vs B v1 r.1 `nami.`; A v1 r.2 `sa,` vs B v1 r.2 `sa`; A v1 r.2 `nami` vs B v1 r.2 `nami.`; A v1 r.3 `nás` vs B v1 r.4 `nás.`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: –; viac v B: `nad`×1, `nami`×1, `Pane,`×1, `sa`×1, `zmiluj`×1
   - V poradí hrania (po rozbalení verseOrder): 12 vs 17 slov, 1 miest s rozdielom obsahu: A `` vs B `Pane, zmiluj sa nad nami.`

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Kyrie` · tituly: `Pane, zmiluj sa nad nami` · verseOrder `v1` · text: nič unikátne
- **B**: tagy: `Anonymous` · tituly: `Pane zmiluj sa nad nami` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.3: `Pane, zmiluj sa nad nami.`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Pane, zmiluj sa nad nami (Kyrie).xml` (A)
- **Zmazať / zlúčiť:** `Pane zmiluj sa nad nami (Anonymous).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B má `Pane, zmiluj sa nad nami.` / `Kriste, zmiluj sa nad nami.` / `Pane, zmiluj sa nad nami.` / `Vyslyš nás.` (17 slov); A iba `Pane, zmiluj sa nad nami`, `Kriste, zmiluj sa, nad nami`, `Vyslyš nás` (12 slov) – chýba 3. vzývanie.
  - A má tag `Kyrie` (patrí do sady Kyrie), B zástupný `Anonymous`; A má `verseOrder` `v1`.
  - A má čiarku navyše: `Kriste, zmiluj sa, nad nami`.
- **Čo prevziať z ostatných:**
  - Do A doplniť 3. vzývanie `Pane, zmiluj sa nad nami.` z B (ak ide o ten istý nápev).
- **Istota:** nízka – Nie je zistiteľné, či ide o ten istý nápev; podľa textu je B úplnejšia.

**Riziká a neistoty:**

- V repozitári existujú rôzne nápevy Kyrie (duplicity.md, časť 5); záleží na melódii.

---

<a id="g52"></a>
## G52 · [4d] `Svätý, svätý (Svätý).xml` · `Svätý,  svätý (Anonymous).xml`

**Zhrnutie:** B má Hosannu raz, A trikrát v blokoch `|: :|`; pravdepodobne iné spracovanie Sanctus; A má preklep `neme`.

**Súbory v skupine:**
- **A** = `Svätý, svätý (Svätý).xml`
- **B** = `Svätý,  svätý (Anonymous).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Svätý, svätý` | `Svätý,  svätý` |
| Tagy (`<author>`) | `Svätý` | `Anonymous` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2` | `v1 v2 c1 v3` |
| Počet slôh / `<lines>` blokov | 2 / 2 | 4 / 4 |
| Počet riadkov (neprázdnych) | 5 (5) | 5 (5) |
| Počet slov (bez čísel slôh) | 31 | 24 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 31 | 24 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 1 |
| Riadky s dvojitou medzerou vnútri | 0 | 2 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 4 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 31 slov v A, 24 slov v B; 3 miest s rozdielom obsahu
1. [chýba v B] A v1 r.3: `hosanna, hosanna` – v B tento text nie je
2. [iný text] A v2 r.1: `neme`  vs  B v3 r.1: `mene`
     - riadok v A: `Požehnaný, Ktorý prichádza v neme Pánovom!`
     - riadok v B: `Požehnaný,  ktorý prichádza v mene Pánovom.`
3. [chýba v B] A v2 r.2: `Hosanna, hosanna, hosanna na výsostiach` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 4, veľkosť písmen: 2
     - interpunkcia: A v1 r.1 `svätý,` vs B v1 r.1 `svätý`; A v1 r.3 `Hosanna,` vs B c1 r.1 `Hosanna`; A v1 r.3 `výsostiach` vs B c1 r.1 `výsostiach!`; A v2 r.1 `Pánovom!` vs B v3 r.1 `Pánovom.`
     - veľkosť písmen: A v1 r.2 `Zem` vs B v2 r.1 `zem`; A v2 r.1 `Ktorý` vs B v3 r.1 `ktorý`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `Hosanna,`×5, `na`×1, `neme`×1, `výsostiach`×1; viac v B: `mene`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Svätý` · tituly: `Svätý, svätý` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.3: `hosanna, hosanna`; v2 r.1: `neme`; v2 r.2: `Hosanna, hosanna, hosanna na výsostiach`
- **B**: tagy: `Anonymous` · tituly: `Svätý,  svätý` · text (slová, ktoré v žiadnom inom súbore nie sú): v3 r.1: `mene`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** obe – `Svätý, svätý (Svätý).xml` + `Svätý,  svätý (Anonymous).xml` (A a B)
- **Zmazať / zlúčiť:** nič.
- **Prečo:**
  - A má `|: Hosanna, hosanna, hosanna na výsostiach :|` v v1 aj v v2 (31 slov), B len `Hosanna na výsostiach!` raz v `c1` (24 slov).
  - A má preklep `Požehnaný, Ktorý prichádza v neme Pánovom!` (v2 r.1) – B má `v mene Pánovom`.
  - B má dvojité medzery v titule `Svätý,  svätý` a v texte, A titul `Svätý, svätý`.
  - A má tag `Svätý`, B zástupný `Anonymous`.
- **Čo prevziať z ostatných:**
  - V A opraviť `neme` → `mene` bez ohľadu na rozhodnutie o zlúčení.
- **Istota:** nízka – Text sa líši v počte Hosanna, takže môže ísť o rôzne nápevy; z dát to nepoznáme.

**Riziká a neistoty:**

- Nepotvrdená zhoda nápevu.

---

<a id="g53"></a>
## G53 · [4d] `Otče náš (Otče náš).xml` · `Otče náš (Večeradlo s Pannou Máriou).xml` · `Otce nas (detsky zbor).xml`

**Zhrnutie:** Tri zápisy Otče náš s rovnakým textom; A má preklep `myodpúšťame`, C chýba `Amen` a má natiahnuté `zlé-é ho`.

Existuje aj verzia s akordmi: `Otce nas (akordy).xml`, ponechaná zámerne (z porovnania vynechaná).

**Súbory v skupine:**
- **A** = `Otče náš (Otče náš).xml`
- **B** = `Otče náš (Večeradlo s Pannou Máriou).xml`
- **C** = `Otce nas (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B | C |
|---|---|---|---|
| Zodpovedá konvencii názvu | áno | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie | nie / nie |
| Tituly | `Otče náš` | `Otče náš` | `Otce nas` |
| Tagy (`<author>`) | `Otče náš` | `Večeradlo s Pannou Máriou` | `detsky zbor` |
| songbooks | – | – | – |
| verseOrder | – | – | – |
| copyright / ccliNo | – / – | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3` | `v1` | `v1` |
| Počet slôh / `<lines>` blokov | 3 / 3 | 1 / 2 | 1 / 1 |
| Počet riadkov (neprázdnych) | 7 (7) | 10 (10) | 9 (9) |
| Počet slov (bez čísel slôh) | 49 | 50 | 50 |
| verseOrder vs dokument | – | – | – |
| Slov po rozbalení verseOrder | 49 | 50 | 50 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 | 0 |
| Riadky s koncovou medzerou | 0 | 1 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 1 | 0 / 0 |
| Konce riadkov súboru | LF | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 49 slov v A, 50 slov v B; 1 miest s rozdielom obsahu
1. [preklep / zmena slova] A v2 r.4: `myodpúšťame`  vs  B v1 r.8: `my odpúšťame`
     - riadok v A: `ako i myodpúšťame svojim vinníkom.`
     - riadok v B: `ako i my odpúšťame svojim vinníkom`
   - Rozdiely len v zápise (rovnaké slová): veľkosť písmen: 6, interpunkcia: 1
     - veľkosť písmen: A v1 r.2 `Tvoje,` vs B v1 r.2 `tvoje,`; A v1 r.2 `príď` vs B v1 r.3 `Príď`; A v2 r.1 `Tvoja` vs B v1 r.4 `tvoja`; A v2 r.1 `Zemi,` vs B v1 r.5 `zemi.`; A v2 r.2 `chlieb` vs B v1 r.6 `Chlieb`; A v3 r.1 `A` vs B v1 r.9 `a`
     - interpunkcia: A v2 r.4 `vinníkom.` vs B v1 r.8 `vinníkom`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `myodpúšťame`×1; viac v B: `my`×1, `odpúšťame`×1

*Dvojica A ↔ C:* 49 slov v A, 50 slov v C; 2 miest s rozdielom obsahu
2. [preklep / zmena slova] A v2 r.4: `myodpúšťame`  vs  C v1 r.7: `my odpúšťame`
     - riadok v A: `ako i myodpúšťame svojim vinníkom.`
     - riadok v C: `ako i my odpúšťame svojím vinníkom`
3. [preklep / zmena slova] A v3 r.1: `zlého. Amen.`  vs  C v1 r.9: `zlé-é ho.`
     - riadok v A: `A neuveď nás do pokušenia, ale zbav nás zlého. Amen.`
     - riadok v C: `ale zbav nás zlé-é ho.`
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 5, veľkosť písmen: 3, diakritika: 1
     - interpunkcia: A v1 r.2 `Tvoje,` vs C v1 r.2 `Tvoje.`; A v2 r.2 `dnes` vs C v1 r.5 `dnes.`; A v2 r.3 `nám` vs C v1 r.6 `nám,`; A v2 r.4 `vinníkom.` vs C v1 r.7 `vinníkom`; A v3 r.1 `nás` vs C v1 r.8 `nás,`
     - veľkosť písmen: A v1 r.2 `príď` vs C v1 r.3 `Príď`; A v2 r.1 `Zemi,` vs C v1 r.4 `zemi`; A v2 r.3 `a` vs C v1 r.6 `A`
     - diakritika: A v2 r.4 `svojim` vs C v1 r.7 `svojím`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `Amen.`×1, `myodpúšťame`×1, `zlého.`×1; viac v C: `ho.`×1, `my`×1, `odpúšťame`×1, `zlé-é`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Otče náš` · tituly: – · text (slová, ktoré v žiadnom inom súbore nie sú): v2 r.4: `myodpúšťame`
- **B**: tagy: `Večeradlo s Pannou Máriou` · tituly: – · text: nič unikátne
- **C**: tagy: `detsky zbor` · tituly: `Otce nas` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.9: `zlé-é ho.`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Otče náš (Otče náš).xml` (A)
- **Zmazať / zlúčiť:** `Otče náš (Večeradlo s Pannou Máriou).xml` (B), `Otce nas (detsky zbor).xml` (C) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Slovne sa A a B líšia len `myodpúšťame` (A, v2 r.4) vs `my odpúšťame` (B, v1 r.8); C má `my odpúšťame`, `zlé-é ho.` (v1 r.9) a nemá `Amen.`
  - A delí text na 3 slohy (2/4/1 riadkov), B má jednu 10-riadkovú sloha s `break="optional"`, C jednu 9-riadkovú.
  - C má `svojím vinníkom` (A, B: `svojim vinníkom`) a titul bez diakritiky `Otce nas`; veľké/malé písmená v B sú nejednotné (`tvoje`/`Tvoje`).
  - Tagy: A `Otče náš`, B `Večeradlo s Pannou Máriou`, C `detsky zbor`.
- **Čo prevziať z ostatných:**
  - V A opraviť `myodpúšťame` → `my odpúšťame`; pridať tagy `Večeradlo s Pannou Máriou`, `detsky zbor`.
- **Istota:** stredná – Text je rovnaký, ale ide o liturgický text, ktorý sa môže používať s rôznym nápevom.

**Riziká a neistoty:**

- Ak sa Otče náš spieva (C má natiahnuté `zlé-é ho`), môže mať iný nápev než odrecitovaný text.

---

<a id="g54"></a>
## G54 · [4d] `Spievaný desiatok (Večeradlo s Pannou Máriou).xml` · `Zdravas Mária (detsky zbor).xml`

**Zhrnutie:** Rovnaký text Zdravas Mária; líši sa `milostiplná` (A) vs `milosti plná,` (B); titul A označuje spievaný desiatok.

**Súbory v skupine:**
- **A** = `Spievaný desiatok (Večeradlo s Pannou Máriou).xml`
- **B** = `Zdravas Mária (detsky zbor).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Spievaný desiatok` | `Zdravas Mária` |
| Tagy (`<author>`) | `Večeradlo s Pannou Máriou` | `detsky zbor` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1` | `v1` |
| Počet slôh / `<lines>` blokov | 1 / 2 | 1 / 1 |
| Počet riadkov (neprázdnych) | 8 (8) | 7 (7) |
| Počet slov (bez čísel slôh) | 32 | 33 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 32 | 33 |
| Riadky s číslom slohy na začiatku (`1.`) | 0 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 1 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 1 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica B ↔ A:* 33 slov v B, 32 slov v A; 1 miest s rozdielom obsahu
1. [preklep / zmena slova] B v1 r.1: `milosti plná,`  vs  A v1 r.1: `milostiplná`
     - riadok v B: `Zdravasʼ, Mária milosti plná,`
     - riadok v A: `Zdravas Mária milostiplná`
   - Rozdiely len v zápise (rovnaké slová): iné: 1, interpunkcia: 4, veľkosť písmen: 2
     - iné: B v1 r.1 `Zdravasʼ,` vs A v1 r.1 `Zdravas`
     - interpunkcia: B v1 r.2 `tebou.` vs A v1 r.2 `tebou,`; B v1 r.4 `tvojho,` vs A v1 r.4 `tvojho`; B v1 r.5 `Mária,` vs A v1 r.5 `Mária`; B v1 r.6 `hriešnych` vs A v1 r.6 `hriešnych,`
     - veľkosť písmen: B v1 r.3 `Požehnaná` vs A v1 r.3 `požehnaná`; B v1 r.6 `teraz` vs A v1 r.7 `Teraz`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v B: `milosti`×1, `plná,`×1; viac v A: `milostiplná`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Večeradlo s Pannou Máriou` · tituly: `Spievaný desiatok` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1: `milostiplná`
- **B**: tagy: `detsky zbor` · tituly: `Zdravas Mária` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.1: `milosti plná,`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** `Zdravas Mária (detsky zbor).xml` (B)
- **Zmazať / zlúčiť:** `Spievaný desiatok (Večeradlo s Pannou Máriou).xml` (A) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - Slovný rozdiel je len `Zdravas Mária milostiplná` (A, v1 r.1) vs `Zdravasʼ, Mária milosti plná,` (B, v1 r.1); zvyšok je rovnaký (32 : 33 slov).
  - B má bežnejšie znenie `milosti plná` a vkladá do slova `Zdravasʼ` znak U+02BC (modifikátor apostrof), ktorý sa môže zle zobraziť.
  - A má titul `Spievaný desiatok` a tag `Večeradlo s Pannou Máriou` (označujú použitie pri spievanom desiatku), B titul `Zdravas Mária` a tag `detsky zbor`.
- **Čo prevziať z ostatných:**
  - Do B pridať tag `Večeradlo s Pannou Máriou` a druhý titul «Spievaný desiatok»; znak U+02BC nahradiť čiarkou.
- **Istota:** nízka – Text je takmer rovnaký, ale nevieme, či ide o ten istý nápev.

**Riziká a neistoty:**

- Rozhodnutie závisí od toho, či sa „Spievaný desiatok“ spieva inak než „Zdravas Mária“.

---

<a id="g55"></a>
## G55 · [4d] `217. (Duch svätý, JKS).xml` · `Pieseň k Duchu Svätému (Večeradlo s Pannou Máriou).xml`

**Zhrnutie:** B je skrátený výber prvých 3 slôh piesne 217 (55 slov oproti 169 v A) s iným zápisom opakovania.

**Súbory v skupine:**
- **A** = `217. (Duch svätý, JKS).xml`
- **B** = `Pieseň k Duchu Svätému (Večeradlo s Pannou Máriou).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `217.` | `Pieseň k Duchu Svätému` |
| Tagy (`<author>`) | `JKS`, `Duch svätý` | `Večeradlo s Pannou Máriou` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4 v5 v6 v7` | `v1 v2 v3 c1` |
| Počet slôh / `<lines>` blokov | 7 / 7 | 4 / 4 |
| Počet riadkov (neprázdnych) | 35 (35) | 14 (14) |
| Počet slov (bez čísel slôh) | 169 | 55 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 169 | 55 |
| Riadky s číslom slohy na začiatku (`1.`) | 7 | 0 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 7 | 0 |
| Riadky s dvojitou medzerou vnútri | 1 | 1 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 14 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 169 slov v A, 55 slov v B; 4 miest s rozdielom obsahu
1. [iný text] A v1 r.4–5: `Príď k nám, príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`  vs  B v1 r.4: `žiaru svetla pravého.`
2. [iný text] A v2 r.4–5: `Príď k nám, príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`  vs  B v2 r.4: `svetlo srdca bôľneho.`
3. [chýba v A (opakovanie vypísané v B)] B v3 r.3: `Ty sladké občerstvenie,` – v A tento text nie je  [JKS1/2/3: JKS1✓ JKS2✓ JKS3✓]
4. [chýba v B] A v4 r.1 – v7 r.5: `V práci si poľahcenie, v sparne si ovlaženie, v plači si potešenie. Príď k … (97 slov)` – v B tento text nie je
   - Rozdiely len v zápise (rovnaké slová): interpunkcia: 5, veľkosť písmen: 6, diakritika: 2
     - interpunkcia: A v1 r.1 `Svätý,` vs B v1 r.1 `Svätý`; A v1 r.2 `seba` vs B v1 r.2 `seba.`; A v1 r.3 `pravého.` vs B v1 r.3 `pravého,`; A v2 r.1 `nám,` vs B v2 r.1 `nám`; A v3 r.2 `Spasiteľ;` vs B v3 r.2 `Spasiteľ,`
     - veľkosť písmen: A v1 r.3 `žiaru` vs B v1 r.3 `Žiaru`; A v2 r.2 `Darca` vs B v2 r.2 `darca`; A v2 r.3 `svetlo` vs B v2 r.3 `Svetlo`; A v3 r.1 `tešiteľ,` vs B v3 r.1 `Tešiteľ,`; A v3 r.3 `ty` vs B v3 r.4 `Ty`; A v3 r.5 `presvätý.` vs B c1 r.2 `Presvätý.`
     - diakritika: A v2 r.3 `bôlneho.` vs B v2 r.3 `bôľneho,`; A v3 r.2 `ta` vs B v3 r.2 `ťa`
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `Bez`×1, `človek`×1, `čo`×2, `dobrého.`×1, `Duchu`×12, `duše`×1, `hriešnosti,`×1, `je`×3, `k`×18, `ľudu`×1, `milosti`×1, `nám,`×18, `naplň`×1, `nič`×1, `nie`×1, `ňom`×1, `Očist`×1, `ovlaženie,`×1, `plači`×1, `plné`×1, `poľahcenie,`×1, `pomocnej`×1, `potešenie.`×1, `práci`×1, `pramene,`×1, `presvätý.`×6, `príď`×18, `radosti,`×1, `ranené.`×1, `si`×3, `sparne`×1, `Svätý,`×6, `tebe`×1, `temnosti,`×1, `uzdrav,`×1, `V`×5, `verného.`×1, `zaviaž,`×1, `žije`×1, `znavené,`×1; viac v B: `bôlneho.`×1, `občerstvenie.`×1, `pravého.`×1, `sladké`×1, `svetla`×1, `ty`×1, `žiaru`×1

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Duch svätý`, `JKS` · tituly: `217.` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.4–5: `Príď k nám, príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`; v2 r.4–5: `Príď k nám, príď k nám, Duchu Svätý, príď k nám Duchu presvätý.`; v4 r.1 – v7 r.5: `V práci si poľahcenie, v sparne si ovlaženie, v plači si potešenie. Príď k nám, príď … (97 slov)`
- **B**: tagy: `Večeradlo s Pannou Máriou` · tituly: `Pieseň k Duchu Svätému` · text (slová, ktoré v žiadnom inom súbore nie sú): v1 r.4: `žiaru svetla pravého.`; v2 r.4: `svetlo srdca bôľneho.`; v3 r.3: `Ty sladké občerstvenie,`

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3, len referencia)**

| Referencia | A | B |
|---|---|---|
| `217. Duchu Svätý, príď z neba (JKS1).xml` (115 slov, slohy: v1 v2 v3 v4 v5 v6 v7) | 169 slov, rozdiel 60 (zhoda 64 %) | 55 slov, rozdiel 89 (zhoda 23 %) |
| `217. Duchu Svätý, príď z neba (JKS2).xml` (164 slov, slohy: v1 v2 v3 v4 v5 v6 v7 v8 v9 v10) | 169 slov, rozdiel 70 (zhoda 59 %) | 55 slov, rozdiel 140 (zhoda 15 %) |
| `217. Duchu Svätý, príď z neba (JKS3).xml` (169 slov, slohy: v1 v2 v3 v4 v5 v6 v7) | 169 slov, rozdiel 1 (zhoda 99 %) | 55 slov, rozdiel 123 (zhoda 27 %) |

**Odporúčanie**

- **Ponechať:** `217. (Duch svätý, JKS).xml` (A)
- **Zmazať / zlúčiť:** `Pieseň k Duchu Svätému (Večeradlo s Pannou Máriou).xml` (B) – po prenesení bodov z „Čo prevziať“.
- **Prečo:**
  - B má iba slohy 1–3 (v1–v3) a refrén `c1` na konci; A má všetkých 7 slôh s refrénom `Príď k nám, príď k nám, Duchu Svätý, príď k nám Duchu presvätý.` pod každou.
  - Opakovanie B zapisuje vypísaním (`Žiaru svetla pravého,` / `žiaru svetla pravého.`), A značkou `|: žiaru svetla pravého. :|`.
  - B má opravenejšie tvary `bôľneho` a `poslal ťa nám`, A má `bôlneho` a `poslal ta nám`; JKS3 (217) má `bôľneho` a `ťa nám`, JKS2 `bôľneho`.
  - B má tag `Večeradlo s Pannou Máriou` a titul `Pieseň k Duchu Svätému`, ktorý A nemá (A má titul len `217.`).
- **Čo prevziať z ostatných:**
  - Do A pridať tag `Večeradlo s Pannou Máriou`, druhý titul «Pieseň k Duchu Svätému» a opravy `bôlneho` → `bôľneho`, `ta nám` → `ťa nám` (nezávisle od skupiny 3). Po zlúčení skupín 3 a 55 by mal súbor tagy «Duch svätý, JKS, Večeradlo s Pannou Máriou, detsky zbor».
- **Istota:** vysoká – B je podmnožina A v obsahu slôh.

**Riziká a neistoty:**

- Skupina 3 mení tú istú pieseň (217); obe zlúčenia robiť naraz, aby sa názov súboru nemenil dvakrát.

---

<a id="g56"></a>
## G56 · [4d] `Keď sa raz Pán navráti k nám (Veľkonočná).xml` · `Keď sa raz Pán ... short (Prijímanie).xml`

**Zhrnutie:** B je zámerne skrátená verzia (5 z 8 slôh, titul s `short`); A je úplná.

**Súbory v skupine:**
- **A** = `Keď sa raz Pán navráti k nám (Veľkonočná).xml`
- **B** = `Keď sa raz Pán ... short (Prijímanie).xml`

**Metadáta, štruktúra, zarovnanie**

|  | A | B |
|---|---|---|
| Zodpovedá konvencii názvu | áno | áno |
| Nezlomiteľná medzera (U+00A0) v názve súboru / titule | nie / nie | nie / nie |
| Tituly | `Keď sa raz Pán navráti k nám` | `Keď sa raz Pán ... short` |
| Tagy (`<author>`) | `Veľkonočná` | `Prijímanie` |
| songbooks | – | – |
| verseOrder | – | – |
| copyright / ccliNo | – / – | – / – |
| Slohy v poradí dokumentu | `v1 v2 v3 v4 v5 v6 v7 v8` | `v1 v2 v3 v4 v5` |
| Počet slôh / `<lines>` blokov | 8 / 8 | 5 / 5 |
| Počet riadkov (neprázdnych) | 32 (32) | 20 (20) |
| Počet slov (bez čísel slôh) | 164 | 92 |
| verseOrder vs dokument | – | – |
| Slov po rozbalení verseOrder | 164 | 92 |
| Riadky s číslom slohy na začiatku (`1.`) | 8 | 5 |
| Číslo slohy zlepené so slovom (`1Duchu`) | 0 | 0 |
| Text omylom v `<chord>` (chyba formátu) | – | – |
| Riadky s koncovou značkou (`… 1.`) | 0 | 0 |
| Riadky s dlhým radom medzier (3+) | 0 | 0 |
| Prázdne riadky (`<br/><br/>`) | 0 | 0 |
| Riadky s koncovou medzerou | 1 | 0 |
| Riadky s dvojitou medzerou vnútri | 0 | 0 |
| Značky opakovania (`/: :/`, `[: :]`, …) | 0 | 0 |
| Vložené `<p>` / `break="optional"` | 0 / 0 | 0 / 0 |
| Konce riadkov súboru | LF | LF |

**Pokyny / zátvorky / značky v texte (môžu sa zobraziť na slajde):** žiadne

**Rozdiely v texte** (porovnanie slovo po slove, bez ohľadu na diakritiku, veľkosť písmen a interpunkciu; poloha = sloha, riadok v rámci slohy)

*Dvojica A ↔ B:* 164 slov v A, 92 slov v B; 2 miest s rozdielom obsahu
1. [chýba v B] A v4 r.1 – v6 r.1: `po mene nazve nás Pán, keď po mene nazve nás Pán, aby by sme … (45 slov)` – v B tento text nie je
2. [chýba v B] A v8 r.1–4: `Keď sa raz Pán navráti k nám, keď sa raz Pán navráti k nám, … (27 slov)` – v B tento text nie je
   - Žiadne rozdiely v zápise (diakritika / veľkosť / interpunkcia) pri zhodných slovách.
   - Početnosť slov bez ohľadu na poradie (po zložení diakritiky): viac v A: `aby`×3, `boli,`×3, `by`×3, `hrob,`×3, `k`×3, `Keď`×9, `mene`×3, `nám,`×3, `nás`×3, `navráti`×3, `nazve`×3, `opustia`×3, `Pán`×6, `po`×3, `raz`×3, `sa`×3, `sme`×3, `svätí`×3, `svoj`×3, `tam`×3, `tiež`×3; viac v B: –

**Unikátny obsah** (čo by sa po zmazaní stratilo)

- **A**: tagy: `Veľkonočná` · tituly: `Keď sa raz Pán navráti k nám` · text (slová, ktoré v žiadnom inom súbore nie sú): v4 r.1 – v6 r.1: `po mene nazve nás Pán, keď po mene nazve nás Pán, aby by sme tiež tam … (45 slov)`; v8 r.1–4: `Keď sa raz Pán navráti k nám, keď sa raz Pán navráti k nám, aby by … (27 slov)`
- **B**: tagy: `Prijímanie` · tituly: `Keď sa raz Pán ... short` · text: nič unikátne

**Porovnanie s referenčnými importmi (JKS1/JKS2/JKS3):** nie je k dispozícii (pieseň nemá číslo v hymnári).

**Odporúčanie**

- **Ponechať:** obe – `Keď sa raz Pán navráti k nám (Veľkonočná).xml` + `Keď sa raz Pán ... short (Prijímanie).xml` (A a B)
- **Zmazať / zlúčiť:** nič.
- **Prečo:**
  - B obsahuje slohy 1, 2, 3, 6, 7 z A (číslované znova ako 1–5); A má navyše slohy `Keď po mene nazve nás Pán` (v4) a `Keď svätí svoj opustia hrob` (v5) a záverečné opakovanie 1. slohy (v8).
  - Text spoločných slôh je slovo po slove rovnaký (rozdiel 0).
  - B má v titule explicitne `short` (`Keď sa raz Pán ... short`) a tag `Prijímanie`, A tag `Veľkonočná`.
- **Čo prevziať z ostatných:** nič.
- **Istota:** stredná – Skrátená verzia je pomenovaná zámerne; alternatívou je jeden súbor s `verseOrder`.

**Riziká a neistoty:**

- Ak sa B zmaže, treba v A pridať `verseOrder` «v1 v2 v3 v6 v7» (číslovanie slôh v texte sa však nezmení).

---

