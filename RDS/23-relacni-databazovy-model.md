**Osnova (this might need more work):**

- vlastnosti relace
- relační integrita
- klíče relace (kandidátní, primární, přirozený, umělý, jednoduchý, složený klíč)
- multiplicita vztahů (multiplicita, kardinalita, participace)
- praktické - normalizace

# Relační datový model

- je nejrozšířenějším způsobem uložení dat v databázích. Jedná se o způsob uložení v logickém smyslu.
- navržen v r. 1969 britským vědcem Edgarem Frankem Coddem (IBM). Definoval pojmy entita, atribut, relace. Současně začala firma pracovat na vývoji jazyka pro ovládání těchto databází - SEQUEL (Structured English Query Language), později přejmenován na SQL. Jednoduchá struktura, data organizována v tabulkách (řádky a sloupce), v tabulkách prováděny veškeré databázové operace.
- dříve se používaly ještě hierarchický nebo síťový model, dnes kromě relačního také objektový a objektově-relační
- nejmladší, v současnosti nejpoužívanější.

Základem relačních databází jsou relace (tabulky), podobné relaci např. v MS Excel. Relace (tabulky) jsou propojené předem nastavenými vztahy. Relace obsahuje jednotlivé atributy = sloupce a řádky = záznamy.

Relační model obecně **realizuje vazbu pomocí relace** , v níž každou entitu do vazby vstupující zastupuje její primární klíč.

V některých případech (vazby 1:1, 1:M) však není nutné použít samostatnou vazební tabulku, ale stačí doplnění tabulky na straně M o další atribut - **cizí klíč**.

**Relační databázové systémy vychází z relačního databázového modelu**. Jde o nejrozšířenější skupinu databázových systém, se kterou se dnes můžeme hodně setkat. Do této skupiny patří například následující databázové systémy: FoxPro, Informix, MS Access, MS SQL, MySQL, Oracle, Postgress, SyBase a WinBase602.

## Vlastnosti relací (tabulek):

Relace má jméno, které je jedinečné v celé databázi

Každá relace musí obsahovat alespoň jeden sloupec, některé relace neobsahují žádné řádky (jsou prázdné).

Každý sloupec má jedinečné jméno v relaci

Všechny hodnoty v jednom sloupci jsou ze stejné domény (mají stejný datový typ)

Nezáleží na pořadí sloupců, sloupce se mohou navzájem zaměňovat

Každý záznam je jedinečný (neexistují duplicitní záznamy)

Nezáleží na pořadí řádků, ale může ovlivnit efektivitu přístupu k záznamům

Každá buňka relace obsahuje přesně jednu hodnotu (je atomická)

## Vlastnosti relačního datového modelu

Z definice relace vyplývají tyto jejich tabulkové vlastnosti:

- homogenita sloupců (prvky domény)
- každý údaj (hodnota atributu ve sloupci) je atomickou položkou
- na pořadí řádků a sloupců nezáleží (jsou to množiny prvků/atributů)
- každý řádek tabulky je jednoznačně identifikovatelný hodnotami jednoho nebo několika atributů (primárního klíče)

## Datové typy

Datový typ určuje, jaké hodnoty se budou moci do daného sloupce zapisovat. Zvolit vhodný datový typ je velice důležité.

V každém sloupci se mohou vyskytovat pouze hodnoty stejného datového typu.

Nesprávný datový typ může způsobit to, že databáze bude velká a že se tím zpomalí.

### Základní datové typy

Mezi základní datové typy patří Text, Datum, Číslo a logická hodnota Ano/Ne (boolean).

**Znak (text)** – libovolné znaky (písmena, číslice a ostatní znaky jako čárky, pomlčky, středníky, závorky atd.). Používá se zejména pro názvy (př. Jméno, Příjmení…) a dále pro uložení všech hodnot, které není možné zařadit do některého dalšího datového typu.

Mohou mít pevnou nebo proměnlivou délku a mívají specifikovanou znakovou sadu.

**Číslo** – pouze číselné hodnoty určitého rozsahu, se znaménkem nebo bez. Rozlišujeme několik druhů číselných datových typů (celé × desetinné). U celých čísel rozlišujeme jejich rozsah (př. 0-255, -32 768 až +32 768 apod.).
U desetinných čísel max. počet platných číslic za des. čárkou.

**Datum** – uchování data v libovolném formátu (DD/MM/RRRR, den-měsíc-rok apod.). Většinou bývá zahrnut i čas.

**Boolean** – speciální formát pro uchování logických hodnot Ano (pravda) a Ne (nepravda). Např. vlastník ŘP apod.

V jednotlivých databázových systémech mohou být použity odlišné názvy pro jednotlivé datové typy

### Číselné datové typy

#### Celočíselné

| Název typu       | Interval                           | Bez znaménka (unsigned) | Paměťový prostor |
| ---------------- | ---------------------------------- | ----------------------- | ---------------- |
| `TINYINT`        | < -128; 127 >                      | < 0; 255 >              | 1 B              |
| `SMALLINT`       | < -32 768; 32 767 >                | < 0; 65 535 >           | 2 B              |
| `MEDIUMINT`      | < - 8 388 608; 8 388 607>          | < 0; 16 777 215 >       | 3 B              |
| `INTEGER`, `INT` | < - 2 147 483 648; 2 147 483 647 > | < 0; 4 294 967 295 >    | 4 B              |
| `BIGINT`         | hodně velké číslo                  | hodně velké číslo       | 8 B              |

#### Reálné

| Název typu      | Interval                       | Bez znaménka (unsigned)        | Paměťový prostor |
| --------------- | ------------------------------ | ------------------------------ | ---------------- |
| `FLOAT(M, D)`   | Liší se podle použitých hodnot | Liší se podle použitých hodnot | 4 B              |
| `DOUBLE(M, D)`  | Liší se podle použitých hodnot | Liší se podle použitých hodnot | 8 B              |
| `DECIMAL(M, D)` | Liší se podle použitých hodnot | Liší se podle použitých hodnot | M+2 B            |

M – celková délka čísla, D – délka čísla za des. čárkou DOUBLE a DECIMAL – používají se pro uložení nepřesných des. čísel. S nepřesnými des. čísly bývají problémy, proto raději používat typ Float (M, D)

![řetězce](/RDS/23-relacni-databazovy-model/retezce.PNG)

### Řetězce

| Název typu   | Maximální velikost | Paměťový prostor |
| ------------ | ------------------ | ---------------- |
| `CHAR(X)`    | 255 B              | X B              |
| `VARCHAR(X)` | 255 B              | X+1 B            |
| `TINYTEXT`   | 255 B              | X+1 B            |
| `TINYBLOB`   | 255 B              | X+2 B            |
| `TEXT`       | 65535 B            | X+2 B            |
| `BLOB`       | 65535 B            | X+2 B            |
| `MEDIUMTEXT` | 1,6 MB             | X+3 B            |
| `MEDIUMBLOB` | 1,6 MB             | X+3 B            |
| `LONGTEXT`   | 4,2 GB             | X+4 B            |
| `LONGBLOB`   | 4,2 GB             | X+4 B            |

### Výčtové datové typy

`ENUM ('prvek1', 'prvek2', ...)` – pole předem definovaných prvků, vybrat můžeme pouze 1 hodnotu, používal se pro ukládání nabídky z roletek na www stránkách raději používat číselníky, tam, kde bychom potřebovali ENUM sloupec s odkazem na cizí klíč

`SET ('prvek1', 'prvek2', ...)` – pole předem definovaných prvků, vybrat můžeme více z def. prvků, ale je problém s indexováním

## Modifikátory datových polí

Klíčová slova, která upravují chování jednotlivých polí tabulky:

| Název modifikátoru | Popis                                                                                                                                                                               | Použití                   |
| ------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| `AUTO_INCREMENT`   | Automatické vložení jedinečného čísla, které se při přidání záznamu do tabulky zvýší o jednu <br>Zjištění nejvyšší hodnoty:<br>`SELECT max(id) FROM tablename`                      | Všechny typy **int**      |
| `DEFAULT`          | Umožňuje změnit implicitní hodnotu pole. Výchozí hodnotou v MySQL je `NULL`                                                                                                         | `CHAR`, `VARCHAR`, `ENUM` |
| `NOT NULL`         | Určuje, že pole musí obsahovat hodnotu                                                                                                                                              | Všechny typy              |
| `NULL`             | Určuje, že pole může obsahovat hodnotu `NULL`                                                                                                                                       | Všechny typy              |
| `PRIMARY KEY`      | Primární klíč - hodnota, která jedinečným způsobem identifikuje každý záznam v tabulce. Nedovoluje hodnotu NULL a musí zároveň mít jedinečný index - musíme zároveň použít `UNIQUE` | Všechny typy              |
| `UNIQUE`           | Zajišťuje integritu klíčem, který není primární. Nesmí obsahovat duplicitní hodnoty.                                                                                                | Všechny typy              |
| `UNSIGNED`         | Definuje pole, do kterého můžeme ukládat pouze kladná čísla. Automaticky posunuje interval povolenych hodnot pro daný datový typ do kladné osy.                                     | Číselné typy              |
| `ZEROFILL`         | Používá se k zobrazení vedoucích nul u čísel, která vyžadují určitý počet cifer (0012)                                                                                              | Číselné typy              |
