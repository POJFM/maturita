# Sekvenční logické obvody

## definice a rozdělení, typy

Hodnoty **výstupních** signálů závisí na okamžitých **hodnotách vstupních proměnných**, a navíc ještě na **hodnotách předchozích**.

Sekvenční obvody se od kombinačních liší => **Pamětí a zpětnými vazbami**(smyčky)

Sekvenční obvod má **vstupní, výstupní a vnitřní proměnné**, ty dávají informace o **předchozích stavech**

<p align="center">
  <img src="img/11-01.png" />
</p>

### Rozdělení Sekvenčních logický obvodů:

1. Bistabilní klopné obvody
2. Monostabilní klopné obvody 
3. Astabilní klopné obvody 

## bistabilní klopné obvody a popis hodinového signálu

### 1. Bistabilní klopné obvody:

Úkol: **Zaznamenat přechodné informace a uchovat jejich stav**, i po zmizení informací ze vstupu

Klopné obvody neboli **flip-flop** - mají **dva stabilní** stavy (0, 1); jeden stabilní stav přechází skokem v druhý.

Nejmenší paměť s kapacitou **1 bit**.

#### Využití:

- paměť 
- tvoří základ složitých sekvenčních obvodů – registry, čítače, časovače, apod.

#### Typy Bistabilních obvodů:

- Asynchronní KO - RS
- Synchronní KO - RS(Latch), JK(derivační), D, T

### Asynchronní Klopné obvody

KO nemusí být řízen dalším vstupem (náběžnou/sestupnou hranou nebo hodinovým signálem Latch)

Nejsou řízené taktovacími impulsy

<p align="center">
  <img src="img/11-02.png" />
</p>

#### Hazardní stav

Přivedeme-li na oba vstupy signál 1 (zakázaný stav) => nastaví se oba výstupy nejprve do stavu 0 =>
konečný stav bude záležet na zpoždění použitých členů, nebo na tom, který ze signálů R a S dříve skončí.
