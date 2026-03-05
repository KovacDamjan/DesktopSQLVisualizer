# DesktopSQLVisualizer - Uporabniski Prirocnik

Verzija: 1.0.13

## 1. Pregled aplikacije

DesktopSQLVisualizer je namizna aplikacija za SQL delo nad bazami:

- MSSQL
- MySQL
- PostgreSQL
- DB2

Glavni zavihki:

- Connections
- SQL Workspace
- ER Diagram

![Glavni pogled aplikacije](images/02.png)

## 2. Connections

V zavihku **Connections** nastavite novo ali obstojeco povezavo:

1. Kliknite **New**.
2. Vnesite Name, Engine, Host, Port, Username, Password.
3. Kliknite **Test connection**.
4. Po potrebi kliknite **Load databases**.
5. Kliknite **Save connection**.
6. Kliknite **Open SQL Workspace**.

![Connections](images/08.png)

## 3. SQL Workspace

V SQL editorju so na voljo:

- **Max rows**
- **Format**
- **Params**
- **Hide Params / Show Params**
- **Explain**
- **Execute**
- **Cancel** (med izvajanjem)

![SQL editor in parametri](images/10.png)

### Izvajanje poizvedbe

- Ce oznacite del SQL, se izvede samo oznaceni del.
- Ce ni oznacenega dela, se izvede celoten SQL iz editorja.

Bliznjica:

- `Ctrl/Cmd + Enter` -> Execute

### Explain

Gumb **Explain** pripravi razlago plana izvedbe poizvedbe (odvisno od baze/engine).
Uporabno za:

- analizo pocasnih poizvedb,
- preverjanje index uporabe,
- primerjavo sprememb po optimizaciji SQL.

Explain rezultat je prikazan kot **drevesni pogled** in vsebuje:

- ime operatorja,
- objekt (ce je na voljo),
- metrike noda (cost/rows),
- dodatno vrstico s podrobnostmi (predicate/keys/access).

Drevesni Explain je na voljo za MSSQL, MySQL, PostgreSQL in DB2.

V **Settings -> Diagnostics** lahko nastavite **Explain details**:

- **Compact**: krajsi, bolj pregleden izpis,
- **Full**: poln izpis podrobnosti po nodih.

### Max rows

Polje **Max rows** doloca najvecje stevilo vrstic, ki se nalozijo za vsak resultset.
Priporocilo:

- za hitrejse delo pri velikih tabelah uporabite nizjo vrednost (npr. 500),
- za analizo vecjih izpisov povecajte vrednost pred Execute.

### Format SQL

Gumb **Format** poravna SQL zapis (odmiki, keyword format), da je poizvedba bolj berljiva.

### Parametri in nacin dela samo v editorju

- **Params (N)** zazna parametre v trenutnem SQL.
- **Hide Params** skrije panel s parametri, da lahko delate neposredno v editorju.
- **Show Params** ponovno prikaze panel.
- Prikaz/skritje parametrov se shrani tudi po ponovnem zagonu aplikacije.
- Ce je parametrov veliko, se zgornji SQL del samodejno poveca, da editor ostane viden.

## 4. Rezultati (multi-resultset)

Po izvedbi se rezultati prikazejo spodaj:

- vec resultsetov (`Result 1`, `Result 2`, ...),
- iskanje po rezultatih,
- sortiranje po stolpcih,
- izvoz v Excel.

![Rezultati in resultset zavihki](images/01.png)

### Messages panel

V **Messages** delu so prikazane:

- informacije o izvajanju,
- opozorila in napake,
- stevilo vrnjenih vrstic,
- cas izvajanja.

To je prvi del, ki ga preverite ob napaki poizvedbe.

## 5. Urejanje podatkov (Edit Mode)

Ce je rezultat urejljiv:

1. Kliknite **Enable Edit Mode**.
2. Spremenite vrednosti.
3. Kliknite **Apply**.

![Edit mode in Apply](images/07.png)

#### Uporaba Edit Mode

- **Enable Edit Mode** vklopi urejanje v mrezi.
- **Target table** doloci tabelo za update (ce je ne zazna samodejno).
- **Key columns** dolocijo kljuce za identifikacijo vrstice (npr. `id`).
- **Apply** izvede spremembe v bazi.

Ce vrstica ni pravilno identificirana po kljucu, update ne bo uspel.

## 6. Database Objects

Levi panel vsebuje:

- Tables
- Functions
- Procedures

Klik na objekt vstavi SQL predlogo v editor.

![Database Objects](images/03.png)

Uporaba:

- hitri klik na tabelo vstavi predlogo poizvedbe,
- pri funkcijah/procedurah se vstavi primeren SQL stavek.

## 7. Favorites in Recent History

Za hitrejse delo lahko uporabljate:

- **Favorites** za pogosto uporabljene SQL poizvedbe,
- **Recent History** za zadnje izvedene poizvedbe.

![Favorites](images/06.png)
![Recent History](images/05.png)

Priporocena uporaba:

- v **Favorites** shranite stabilne SQL poizvedbe (porocila, kontrole),
- v **Recent History** hitro vrnete zadnje poizvedbe in parametre.

## 8. Autocomplete

Monaco editor podpira kontekstni autocomplete za:

- SQL keywords,
- sheme in tabele,
- funkcije/procedure,
- stolpce (glede na kontekst poizvedbe).

Namig:

- autocomplete odprete tudi ročno z `Ctrl/Cmd + Space`.

![Autocomplete v editorju](images/11.png)

## 9. Command Palette (F1)

S tipko **F1** odprete command palette editorja.

V aplikaciji so na voljo SQL ukazi, npr.:

- SQL: Execute
- SQL: Explain
- SQL: Format SQL
- SQL: Detect Parameters
- SQL: Reload Database Objects

Uporaba:

1. Pritisnite **F1**.
2. Vnesite `>sql`.
3. Izberite ukaz.

![Command palette](images/12.png)

## 10. ER Diagram

V zavihku **ER Diagram** lahko:

- pregledate tabele in relacije,
- uporabljate search/focus,
- osvezite model,
- uporabite Auto Layout.

![ER Diagram](images/09.png)

## 11. Posodobitve aplikacije

V zgornji vrstici je prikazan status posodobitev in verzija aplikacije.

Primer statusa:

- `Updated`
- `Downloading update`
- `Update ready`

![Status posodobitve](images/04.png)

## 12. Najpogostejse tezave

### Povezava ne uspe

Preverite:

- host/port,
- uporabnisko ime/geslo,
- pravilen engine.

### Premalo vrstic v rezultatu

Povecajte **Max rows** in poizvedbo izvedite znova.

### Tezave s tipi parametrov na DB2

Ce procedura na DB2 zahteva specificen tip (npr. array ali numeric), uporabite:

- tip parametra iz metadata procedure v panelu Params,
- po moznosti named parametre (`:param`),
- array vrednosti v podprtih oblikah (`{1,2}`, `[1,2]` ali typed array syntax, ce ga procedura zahteva).

### Podpora

Pri prijavi tezave posredujte:

- ime povezave,
- SQL poizvedbo (ce je mozno),
- besedilo napake iz Messages,
- korake za ponovitev tezave.
