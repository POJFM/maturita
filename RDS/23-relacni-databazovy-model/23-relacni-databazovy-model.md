**Relační datový model**  je nejrozšířenějším způsobem uložení dat v databázích. Jedná se o způsob uložení v logickém smyslu.

-jeden z nejpoužívanějších modelů

- navržen v r. 1969 britským vědcem Edgarem Frankem Coddem (IBM). Definoval pojmy entita, atribut, relace. Současně začala firma pracovat na vývoji jazyka pro ovládání těchto databází - SEQUEL (Structured English Query Language), později přejmenován na SQL. Jednoduchá struktura, data organizována v tabulkách (řádky a sloupce), v tabulkách prováděny veškeré databázové operace.

- dříve se používaly ještě hierarchický nebo síťový model, dnes kromě relačního také objektový a objektově-relační

-nejmladší, v současnosti nejpoužívanější. 

Základem relačních databází jsou relace (tabulky), podobné relaci např. v MS Excel. Relace (tabulky) jsou propojené předem nastavenými vztahy. Relace obsahuje jednotlivé atributy = sloupce a řádky = záznamy.

Relační model obecně **realizuje vazbu pomocí relace** , v níž každou entitu do vazby vstupující zastupuje její primární klíč.

V některých případech (vazby 1:1, 1:M) však není nutné použít samostatnou vazební tabulku, ale stačí doplnění tabulky na straně M o další atribut - **cizí klíč**.

**Relační databázové systémy vychází z relačního databázového modelu**. Jde o nejrozšířenější skupinu databázových systém, se kterou se dnes můžeme hodně setkat. Do této skupiny patří například následující databázové systémy: FoxPro, Informix, MS Access, MS SQL, MySQL, Oracle, Postgress, SyBase a WinBase602.



**Vlastnosti relací (tabulek):**

 Relace má jméno, které je jedinečné v celé databázi

 Každá relace musí obsahovat alespoň jeden sloupec, některé relace neobsahují žádné řádky (jsou prázdné).

 Každý sloupec má jedinečné jméno v relaci

 Všechny hodnoty v jednom sloupci jsou ze stejné domény (mají stejný datový typ)

 Nezáleží na pořadí sloupců, sloupce se mohou navzájem zaměňovat

 Každý záznam je jedinečný (neexistují duplicitní záznamy)

 Nezáleží na pořadí řádků, ale může ovlivnit efektivitu přístupu k záznamům

 Každá buňka relace obsahuje přesně jednu hodnotu (je atomická)

**Vlastnosti relačního datového modelu**

Z definice relace vyplývají tyto jejich tabulkové vlastnosti:

- homogenita sloupců (prvky domény)
- každý údaj (hodnota atributu ve sloupci) je atomickou položkou
- na pořadí řádků a sloupců nezáleží (jsou to množiny prvků/atributů)
- každý řádek tabulky je jednoznačně identifikovatelný hodnotami jednoho nebo několika atributů (primárního klíče)

**Datové typy**

Datový typ určuje, jaké hodnoty se budou moci do daného sloupce zapisovat. Zvolit vhodný datový typ je velice důležité.

V každém sloupci se mohou vyskytovat pouze hodnoty stejného datového typu.

Nesprávný datový typ může způsobit to, že databáze bude velká a že se tím zpomalí.

**Mezi základní datové typy patří** Text, Datum, Číslo a logická hodnota Ano/Ne.

**Znak (text)** – libovolné znaky (písmena, číslice a ostatní znaky jako čárky, pomlčky, středníky, závorky atd.). Používá se zejména pro názvy (př. Jméno, Příjmení…) a dále pro uložení všech hodnot, které není možné zařadit do některého dalšího datového typu.

Mohou mít pevnou nebo proměnlivou délku a mívají specifikovanou znakovou sadu.

**Číslo** – pouze číselné hodnoty určitého rozsahu, se znaménkem nebo bez. Rozlišujeme několik druhů číselných datových typů (celé × desetinné). U celých čísel rozlišujeme jejich rozsah (př. 0-255, -32 768 až +32 768 apod.).
 U desetinných čísel max. počet platných číslic za des. čárkou.

**Datum** – uchování data v libovolném formátu (DD/MM/RRRR, den-měsíc-rok apod.). Většinou bývá zahrnut i čas.

**Ano/Ne** – speciální formát pro uchování logických hodnot Ano (pravda) a Ne (nepravda). Např. vlastník ŘP apod.

V jednotlivých databázových systémech mohou být použity odlišné názvy pro jednotlivé datové typy

![celočíselné datové typy](/RDS/23-relacni-databazovy-model/ciselne_typy.PNG)

![reálné datové typy](/RDS/23-relacni-databazovy-model/realne_typy.png)

M – celková délka čísla, D – délka čísla za des. čárkou DOUBLE a DECIMAL – používají se pro uložení nepřesných des. čísel. S nepřesnými des. čísly bývají problémy, proto raději používat typ Float (M, D)

![řetězce](/RDS/23-relacni-databazovy-model/retezce.png)

**VÝČTOVÉ DATOVÉ TYPY**

**ENUM** (´prvek1&#39;, ‚prvek2&#39;,…) – pole předem definovaných prvků, vybrat můžeme pouze 1 hodnotu, používal se pro ukládání nabídky z roletek na www stránkách raději používat číselníky, tam, kde bychom potřebovali ENUM-\&gt; sloupec s odkazem na cizí klíč


SET (´prvek 1&#39;, &#39;prvek2&#39;,…) – pole předem definovaných prvků, vybrat můžeme více z def. prvků, ale je problém s indexováním

**Modifikátory datových polí**

Klíčová slova, která upravují chování jednotlivých polí tabulky:

![modifikatory datovych poli](/RDS/23-relacni-databazovy-model/modifikatory.png)
