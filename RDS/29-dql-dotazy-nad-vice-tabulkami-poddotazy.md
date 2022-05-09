# DQL dotazy nad více tabulkami

## Relační algebra

- Procedurální jazyk
- Skládá se z množiny operací, které jsou uplatňovány na jednu nebo dvě relace
- Výsledkém operace je opět relace

## Základní operace relační algebry

### Projekce

- Vybíráme jen nektěré sloupce
- Snižuje počet atributů v relaci
- Převádí relaci z `N` atributy na relaci s `M` atributy, platí `N > M`
- Nejsou povoleny duplicitní řádky

### Restrikce

- Vyberu jen některé záznamy pomocí podmínky where
- Snižuje počet datových N-tic
- Vybere pouze datové N-tice ze vstupní relace na základě logické podmínky
- Používáme relační operátory `=`, `>`, `<`

### Difference

- Je to binární operace, která se uplatňuje na relace stejného stupně
- Atributy musí být definovány nad stejnými doménami (sloupce musí být stejného datového typu)
- Výsledná relace obsahuje datové N-tice (řádky) první relace, které nejsou v druhé relaci
- Nelze v MySQL přímo vyjádřit

`SELECT a,b FROM Tab1 WHERE (a,b) NOT IN (SELECT C,d FROM Tab2);`

### Sjednocení

- Vstupní relace musí být stejného stupně (stejný počet atributů)
- Všechny atributy musí být ve stejné doméně
- Výsledkem je relace, která obsahuje buď řádky 1., nebo 2. relace
- Duplicitní řádky nejsou povoleny (pokud vzniknou duplicitní řádky, tak se nevypíšou)

`SELECT a,b FROM Tab1 UNION SELECT c,d FROM Tab2;`

- Sjednocení s duplicitními řádky

`SELECT a,b FROM Tab1 UNION ALL SELECT c,d FROM Tab2;`

## Ostatní operace relační algebry

- Jsou to operace, které lze vytvořit i pomocí základních operací

### Průnik

- Binární operace, která se uplatňuje na relace stejného stupně.
- Atributy jsou definovány nad stejnými doménami.
- Bez duplicitních řádků
- Průnik lze také vyjádřit jako vnitřní spojení na rovnost nad všemi atributy vstupní relace (nad všemi sloupci první tabulky) s projekcí nad atributy jedné ze vstupních relací

```
SELECT a,b FROM Tabl WHERE (a,b) IN (SELECT C,d FROM Tab2);
SELECT a,b FROM Tab1, Tab2 WHERE a=c AND b=d;
SELECT FROM Tabl INNER JOIN Tab2 ON a-c AND b=d;
```

### Kartézský součin

- Binární operace, stupeň výsledné relace je `M+N` (kardinalita `M*N`)

`SELECT * FROM Tab1,Tab2;`

### Spojení

- Nejčastější relační operace s 2 relacemi.
- Spojení 2 relací vytvoří jednu výslednou relaci.
- Výsledná relace obsahuje kombinace datových N-tic, jež vyhovují podmínce a druhu spojení.
- Podmínka vyjadřuje vztah mezi relacemi.
- Zajišťuje se pomocí stejného atributu definovaného nad stejnou doménou

#### Vnitřní spojení

- Na rovnost
- Theta spojení => na nerovnost `!= (<>)` nebo další porovnávací operátory `>`, `=`, `<`

#### Vnější spojení

- Levé spojení

`SELECT * FROM Tab1 LEFT OUTER JOIN Tab2 ON a=C;`

- Pravé spojení
  `SELECT * FROM Tab1 RIGHT OUTER JOIN Tab2 ON a=c;`
- Plné spojení
  `SELECT * FROM Tab1 ON a=c FULL OUTER JOIN Tab2 ON a=c;`

## Pod dotazy

- Umožňují výstup jednoho dotazu použít jako vstup jiného dotazu.
- Vnitřní dotaz je součásti vnějšího dotazu.
- Výstup poddotazu vkládáme jako vstup vnějšího dotazu, obvykle do klauzule `WHERE` nebo `HAVING`.
- Poddotaz může ale být kdekoliv ve vnějším dotazu.
- Výhody:
  - Rychlost
  - návaznost
  - strukturovanost
- Nevýhody
  - Pokud je špatně napsaný je pomalý
