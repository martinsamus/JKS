# Duplicity piesní

Stav k 9. 10. 2026. Nahrádza zastaraný `duplicity.csv` (snímka spred prvého čistenia).

Porovnané všetky súbory v `Piesne/`. Text každej piesne bol normalizovaný (bez diakritiky,
interpunkcie, čísel slôh, akordov a opakovacích značiek) a páry piesní sa porovnávali podľa
spoločných 4-slovných úsekov. Predošlé čistenie hľadalo len bajtovo zhodný text alebo rovnaký názov,
preto tieto duplicity nenašlo.

**Legenda:** názvy súborov sú bez `.xml`, všetky sú v `Piesne/`. **Tučne** je navrhnutá verzia na
ponechanie, ostatné súbory v položke sú kandidáti na zmazanie (alebo zlúčenie tagov). Hotové položky
sú odškrtnuté.

## Otvorená otázka: kópie pre detský zbor

44 skupín obsahuje kópiu s tagom `detsky zbor`. Pri prvom čistení sa kópie `detsky zbor` ponechali
voči `Author Unknown`, ale `Modlitba zasvetenia. (detsky zbor)` sa zmazala v prospech verzie
`Veceradlo`. Treba rozhodnúť jeden postup:

1. zmazať kópiu pre detský zbor (lepšia verzia ostane bez zmeny),
2. zlúčiť – ponechať lepšiu verziu a pridať jej autora/tag `detsky zbor` (súbor sa premenuje),
3. ponechať detský zbor ako samostatnú sadu a čistiť len ostatné skupiny.

## 1. V poriadku (bez akcie)

- Žiadne `-N` súbory (`… -1.xml`) z nového exportu.
- **JKS1, JKS2, JKS3**: vo vnútri sady žiadne duplicity ani zdvojené čísla. Jediná podobnosť
  `223a`/`223b` v JKS2 sú zdokumentované varianty. Rovnaké názvy v rámci sady (napr. *Teba, Bože,
  chválime*) sú rôzne piesne pod rôznymi číslami. Zhody JKS ↔ JKS1/2/3 sú zámerné.
- 35 párov `akordy` ↔ `detsky zbor` (známe, ponechané zámerne; vrátane `Všade tam kde sú` z bodu 3).
- Preskoky v číslach slôh v ostatných piesňach sú v poriadku – výber slôh z hymnára (napr. `004.` má
  slohy 1, 2, 9, 10, 11) alebo časti omše s vlastným číslovaním (Ofertórium, Glória, Krédo…).

## 2. Zlé číslovanie

- [x] `048. Dobrá novina, šťastná hodina (JKS, Vianočná)` → prečíslované na **`049.`** (je to
  pieseň č. 49 – značky slôh aj JKS1/2/3; č. 48 je *Dnešný deň sa radujme*). Commit `6414e6d`.
  Duplicita s `049. Dobrá novina (JKS)` ostáva otvorená – pozri 4a.
- [x] `117. Kde je Ježiš, moja žiadosť (JKS)` – značky slôh `116.` → `117.`
- [x] `212. Hľa, žiarou skvie sa Kristov hrob (JKS, Veľkonočná)` – 2. a 3. sloha `211` → `212.`
- [x] `228. Nebo i zem, vyhlasujte (Božské Srdce, JKS)` – 8. sloha `227.` → `228.`
- [x] `Ani brat môj, ani sestra (Prijímanie, Pôstna)` – 3. sloha mala číslo `2.`
- [ ] `536. Ctime túto sviatosť slávnu (JKS)` – overiť číslo. V JKS1/JKS2/JKS3 je táto pieseň pod
  č. 317; tlačený JKS má za č. 526 ešte položky bez textu, takže 536 môže byť platný odkaz
  (zdroj nws.sk sa nepodarilo otvoriť).

## 3. Akordové verzie bez tagu `akordy`

Mali akordy, ale autora `Author Unknown` – podľa konvencie z predošlých commitov dostali namiesto
neho tag `akordy` (súbory premenované, nemazať):

- [x] `Ticha noc A-dur (akordy)` – transpozícia `Ticha noc - G-dur (akordy)`
- [x] `Všade tam kde sú (akordy)`
- [x] `Pane zmiluj sa, klasika. (akordy)` – akordová verzia `Pane, zmiluj sa (klasické) (Kyrie)`
- [x] `Nesieme Pane chlieb a vino (akordy)`

## 4. Duplicity v pôvodných piesňach (OpenLP)

Takmer všetko sú skupiny, kde sa líši len formátovanie (interpunkcia, delenie slôh, `/: :/` vs
`|: :|`, názov bez diakritiky), prípadne chýba/pribudne sloha.

### 4a. Piesne z JKS (s číslom)

- [ ] **`049. Dobrá novina, šťastná hodina (JKS, Vianočná)`** · `049. Dobrá novina (JKS)` – identický text
- [ ] **`051. Do hory, do lesa, valasi (JKS, Vianočná)`** · `Do hory do lesa (detsky zbor)` – identický text
- [ ] **`066. Ó, chýr preblahý (JKS, Vianočná)`** · `O chyr Preblahy (detsky zbor)` – rovnaký text, iné opakovania
- [ ] **`088. Tichá noc, svätá noc! (JKS, Vianočná)`** · `Ticha noc - G-dur (detsky zbor)` – identický; akordové verzie G/A-dur ostávajú
- [ ] **`209. Obeť svoju veľkonočnú (JKS, Veľkonočná)`** · `209. Obeť svoju veľkonočnú (bez čísel) (JKS, Veľkonočná)` · `Obet svoju Velkonocnu (detsky zbor)` – identický; „bez čísel“ je asi zámerná verzia bez značiek slôh (má preklep „Galiley“)
- [ ] **`217. (Duch svätý, JKS)`** · `Duchu Svätý, príď z neba (detsky zbor)` – rovnaký text (v detskom zbore refrén ako `c1` + „atď.“); 217 nemá v názve meno piesne
- [ ] **`244. K stolu božej láskavosti (JKS, Začiatok)`** · `244 jks (detsky zbor)` – identický text
- [ ] **`039. Búvaj, Dieťa krásne (JKS, Vianočná)`** · `Buvaj dieta krasne A-dur jednoduchy (detsky zbor)` – rovnaký text (detský zbor má delené slabiky „mi-lý“)
- [ ] **`295. Vitaj, milý Jezu Kriste (Eucharistické, JKS)`** · `JKS Vitaj milý Jezu (detsky zbor)` – detskému zboru chýba 6. sloha
- [ ] **`484. Yzopom ma pokrop Pane (JKS)`** · `Yzopom (detsky zbor)` – detský zbor má len 2 zo 4 slôh
- [ ] **`365 (JKS)`** · `365 Pod tvoj plášť sa utiekame, (JKS)` – druhá má len 4 zo 7 slôh
- [ ] `419. K tebe prichádzame (JKS)` · `JKS 419 - K tebe prichádzame (JKS)` – `419.` má 2 slohy, „JKS 419 -“ má 3 (ako JKS2); návrh: doplniť 3. slohu do `419.` a zmazať „JKS 419 -“
- [ ] **`536. Ctime túto sviatosť slávnu (JKS)`** · `JKS 536 - Ctíme túto sviatosť slávnu (JKS)` – rovnaký text (pri prvom čistení ostalo „536.“)
- [ ] **`141. Môj Otče (Komunita Emanuel)`** · `Moj otče (Anonymous)` – identický; Anonymous má všetko v 1 slohe

### 4b. Žalmové odpovede

- [ ] **`Ž 30 (JKS)`** · `žalm (Author Unknown)` – identická veta
- [ ] **`Pane zošli svojho Ducha a obnov tvárnosť zeme (Zalm)`** · `Ž- Pane zošli svojho Ducha (Author Unknown)` – identická veta

### 4c. Ostatné piesne

- [ ] **`Baránok (Večeradlo s Pannou Máriou)`** · `Baranok Bozi-klasika (detsky zbor)` – rovnaký text („zmiluj sa, zmiluj sa“)
- [ ] **`Boh je láska (...)`** · `Boh je láska (Author Unknown)` – AU má v texte „""""""""“
- [ ] **`Bože Otče, teraz vidím (Anonymous)`** · `Bože Otče, teraz vidím (Chvály)` – Anonymous má refrén ako `c1`
- [ ] **`Čakajú ťa nástrahy (Mariánska)`** · `Čakajú ťa nástrahy (Anonymous)` · `Cakaju ta nastrahy (detsky zbor)`
- [ ] **`Chválim Ťa Ježiš (Chvály)`** · `Chválim ťa, Ježiš (Večeradlo s Pannou Máriou)` · `Chvalim Ta Jezis (detsky zbor)` · `Chválim tav Jezis (detsky zbor)` – **2 kópie aj v rámci detského zboru**
- [ ] **`Dávam všetko (Adorácia, Obetné dary, Rieka života)`** · `Dávam všetko (...)` · `Dnes chcel by som ti dať (Rieka Života)` · `Dnes chcel by som Ti dat (detsky zbor)` – 4 kópie tej istej piesne
- [ ] **`Do tmy našich dní (Advent, Pomalá, Pôstna, Taize)`** · `Do tmy našich dní (Taize)` – prvá má text vypísaný 2×
- [ ] **`Dobrorečíme Ti (Obetné dary)`** · `Dobrorecime Ti (detsky zbor)` – detský zbor má preklep „ako ako“, ale lepšie delenie (refrén)
- [ ] **`Glória - UPC (Glória)`** · `Gloria_Vinbarg (detsky zbor)` – rovnaký text aj štruktúra
- [ ] **`Jasaj v Pánovi celá Zem (Veľkonočná)`** · `Jasaj v Pánovi (Anonymous)` – iné značenie refrénu
- [ ] **`Je stále prítomná (Advent, Pôstna, Začiatok)`** · `Je stále prítomná (Anonymous)` · `Je stale pritomna (detsky zbor)`
- [ ] **`Ježiš môj (Anonymous)`** · `Jezis moj, pred tvojou stojim obetou (detsky zbor)` – rovnaký text, iné delenie
- [ ] **`Ježiš, ty si skalou (Prijímanie)`** · `Ježiš, ty si skalou (Anonymous)` · `Jezis ty si skalou (detsky zbor)`
- [ ] **`Kríž je znakom spásy (Pôstna, krížová cesta)`** · `Kríž je znakom spásy (Anonymous)` · `Kriz je znakom spasy (detsky zbor)`
- [ ] **`Laudate Dominum (Chvály, Taize)`** · `Laudate Dominum (Taize)` – identický
- [ ] **`Moja múdrosť (Advent, Pomalá, Pôstna, Taize)`** · `Moja múdrosť (Taize)` – identický, iné delenie
- [ ] **`Môj Boh, vďaka tebe dýcham (Prijímanie)`** · `moj boh (detsky zbor)` – Prijímanie má navyše 1 riadok, ale preklep „zmelina“
- [ ] **`Taky Velky Taky maly (detsky zbor)`** · `Môžeš svätým byť (Večeradlo s Pannou Máriou)` – Večeradlu chýba riadok „Aj plešatý aj vlasatý“
- [ ] **`Náš Pán, On je Kráľov Kráľ (Veľkonočná)`** · `Nas Pan_On je kralov Kral (detsky zbor)` – identický
- [ ] **`Nebojim sa (Author Unknown)`** · `Nebojim sa (detsky zbor)` – líšia sa 1 preklepom („potrebujeme“ v detskom zbore)
- [ ] **`Nech vás požehnáva Pán (Author Unknown)`** · `nech vas pozehnava pan (detsky zbor)` · `Požehnanie sv.Františka (Jerichove Trúby, svadobná)` – posledná má v texte pokyny („celé 3x“, „tvá-ááá-ár“)
- [ ] **`Nepoškvrnená Mária (Veceradlo, Večeradlo s Pannou Máriou)`** · `Neposkvrnena (detsky zbor)` – identický
- [ ] **`NEPOŠKVRNENÉ SRDCE MÁRIE (Mariánska, Veceradlo)`** · `Neposkvrnene Srdce Marie (detsky zbor)` – opakovania raz vypísané, raz `[: :]`
- [ ] **`Nesieme, Pane, chlieb a víno (Obetné dary)`** · `Nesieme Pane chlieb a víno (Anonymous)` – identický (akordová verzia `Nesieme Pane chlieb a vino (akordy)`)
- [ ] **`Nežne zlomený (...)`** · `Ku krížu dvíham zrak - Nežne zlomený (Rieka Života)` – RŽ verzia má tú istú slohu 2× (v2 = v3)
- [ ] **`Ty mi dávaš nohy jeleníc (Anonymous)`** · `Nohy jeleníc (Prijímanie)` – líšia sa 1 slovom („duši“/„ceste“)
- [ ] **`Otváram srdce (MaranaTha)`** · `Otváram srdce (...)` · `Srdce dokorán (Anonymous)`
- [ ] **`Padáme na svoju tvár (...)`** · `Padáme na svoju tvár (Anonymous)` – identický; (...) má verseOrder
- [ ] **`Pane, som tak veľmi rád (Veľkonočná)`** · `Pane, som tak veľmi rád (Anonymous)`
- [ ] **`Po Tebe tuzim viac (detsky zbor)`** · `Po tebe túžim viac (Anonymous)` – identický; detský zbor má refrén + verseOrder
- [ ] **`Poď, teraz je čas (Začiatok)`** · `Pod, teraz je cas vzdat chvalu (detsky zbor)`
- [ ] **`Poďme všetci spolu (Rieka Života)`** · `podme vsetci spolu (detský zbor)` · `podme chvalit ho (Anonymous)` – Anonymous má navyše záver „Poďme chváliť ho / Ježiš“
- [ ] **`Prijmi tieto naše dary, Pane (Obetné dary)`** · `Príjmi tieto naše dary (detsky zbor)` – detskému zboru chýba 3. sloha
- [ ] **`Si môj Pán, Ježiš Kráľ (Author Unknown)`** · `si moj pan (Author Unknown)` – „si moj pan“ má chyby v diakritike
- [ ] **`Stretol ma dnes Pán (Prijímanie, Veľkonočná)`** · `Stretol ma dnes pan (detsky zbor)` · `Tak všetci spolu chváľme ho (...)`
- [ ] **`Svätý (Večeradlo s Pannou Máriou)`** · `Svaty - Pane Boze svetov nekonecnych (detsky zbor)`
- [ ] **`Svoj pokoj (...)`** · `Svoj pokoj (Anonymous)` – Anonymous má preklep „spoj pokoj“
- [ ] **`Šťastie (Mariánska)`** · `Je dnes taký zvláštne krásny deň (Mariánska)` – druhej chýba 3. sloha
- [ ] **`Túžim priniesť na oltár (Richard Čanaky)`** · `Obeta srdca (Obetné dary)` · `tuzim priniest (detsky zbor)` – detský zbor má inak posledné 2 riadky
- [ ] **`Ty si Najvyšší, Ty si Pán (Author Unknown)`** · `Ty si najvyssi (detsky zbor)` – detský zbor má preklepy („ponúka“, „svitim“)
- [ ] **`Ty si mojou láskou (detsky zbor)`** · `Ty si mojou láskou (Anonymous)` – Anonymous má preklepy („Aleuja“) a všetko v 1 slohe
- [ ] **`Ty si Pánom, Ty si Kráľom (Prijímanie)`** · `Ty si Pánom (...)` · `Ty si panom, ty si kralom (detsky zbor)`
- [ ] **`Ty si Pane stále pri mne (Anonymous)`** · `Ty si, Pane, stále pri mne (Pôstna)` · `Ty si Pane stale pri mne (detsky zbor)`
- [ ] `Vďaka Ježiš (Richard Čanaky)` · `Vďaka Ježiš (Záver)` – identický; návrh zlúčiť do `Vďaka Ježiš (Richard Čanaky, Záver)`
- [ ] **`Vládca (MaranaTha)`** · `Vladca (detsky zbor)`
- [ ] **`Všade tam kde sú (detsky zbor)`** · `Všade tam kde sú (Anonymous)` · `Privítajme Pána (Začiatok)` – Anonymous má zlepené slová („Ježišv“, „ženáš“); akordová verzia `Všade tam kde sú (akordy)`
- [ ] **`Vznešený (Adorácia)`** · `Vzneseny (detsky zbor)` – identický
- [ ] **`Vždy je s nami tá (Mariánska)`** · `Vždy je s nami tá (Anonymous)`
- [ ] **`ZÁCHRANÁR (Večeradlo s Pannou Máriou)`** · `Zachranar (detsky zbor)`
- [ ] **`Zvelebený Pán (Rieka Života)`** · `Zvelebený buď (detsky zbor)`
- [ ] **`Žalm 131 (Anonymous)`** · `Nasytene dieta - Zalm 131 (detsky zbor)`
- [ ] **`ŽALM (Večeradlo s Pannou Máriou)`** · `spievaj panovi (detsky zbor)`

### 4d. Neisté – liturgické texty a modlitby (môžu to byť rôzne melódie)

- [ ] `Pane, zmiluj sa nad nami (Kyrie)` · `Pane zmiluj sa nad nami (Anonymous)`
- [ ] `Svätý, svätý (Svätý)` · `Svätý,  svätý (Anonymous)`
- [ ] `Otče náš (Otče náš)` · `Otče náš (Večeradlo s Pannou Máriou)` · `Otce nas (detsky zbor)`
- [ ] `Spievaný desiatok (Večeradlo s Pannou Máriou)` · `Zdravas Mária (detsky zbor)`
- [ ] `217. (Duch svätý, JKS)` · `Pieseň k Duchu Svätému (Večeradlo s Pannou Máriou)` – Večeradlo má len 3 slohy a iné opakovanie
- [ ] `Keď sa raz Pán navráti k nám (Veľkonočná)` · `Keď sa raz Pán ... short (Prijímanie)` – zámerne skrátená verzia

## 5. Nie sú duplicity (falošné zhody)

- Rôzne nápevy Kyrie: `Pane zmiluj sa II (detsky zbor)`, `Pane ymiluj sa-moravské (detsky zbor)`,
  `Pane, zmiluj sa (pomalé) (Kyrie)` vs. klasické.
- `Baránok (Anonymous)` vs `Baránok Boží - pomaly (Anonymous)`; `Glória (klasická) (Glória)` vs
  `Glória (vinimini) (Glória)`.
- `Ctime túto Sviatosť (...)` – má navyše refrén „Baránok Boží, spása pre všetkých“.
- `Dusa kristova (detsky zbor)` vs `303. Duša Kristova` – iné spracovanie.
- `Do tmy na svet (Adorácia)` vs `Do tmy na svet (akordy)` a `040. Čas radosti, veselosti (JKS)` vs
  `040. Čas radosti, veselosti (JKS, Vianočná)` – už ponechané zámerne.
- Krátke žalmové odpovede obsiahnuté v `Ž …` súboroch (`Verš Svätý je Boh`, `Čerpajme vodu Ž`,
  `Aleluja (Anonymous)` ↔ `Ž 114`), modlitby v `RUŽENEC`, `002. Anjel Pána`, `Omsa Texty`.

## 6. Ďalšie nálezy (nie duplicity)

- [ ] 15 súborov má v názve nezlomiteľnú medzeru (U+00A0), čo sťažuje vyhľadávanie podľa názvu:
  `003. Anjel z neba v rúchu jasnom (Advent, JKS)`, `016. Oblaky z neba (Advent, JKS)`,
  `021. Roste, nebesá, z výsosti (Advent, JKS)`, `022. Už z neba posol schádza (Advent, JKS)`,
  `025. V spôsobe chleba (Advent, JKS)`, `097. Z Panny Pán Ježiš je narodený (JKS, Vianočná)`,
  `105. Ó, Ježišu, buď k pomoci (JKS)`, `181. Rozjímať o umučení (JKS, krížová cesta)`,
  `219. Leť, prosba naša, k výšinám (Duch svätý, JKS)`, `Kríž je znakom spásy (Pôstna, krížová cesta)`,
  `Poď, teraz je čas (Začiatok)`, `Prijmi tieto naše dary, Pane (Obetné dary)`,
  `Privítajme Pána (Začiatok)`, `Sme z rôznych strán a kútov (Začiatok)`,
  `Čakajú ťa nástrahy (Mariánska)`
- [ ] `Duchu Svätý, príď z neba (detsky zbor)` – v 1. slohe je text „žiaru svetla pravého.:“ uložený
  omylom ako názov akordu (`<chord name="…"/>`), takže sa na snímke nezobrazí. Súbor je zároveň
  kandidát na zmazanie v 4a (duplicita `217.`).
