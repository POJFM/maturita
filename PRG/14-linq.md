# LINQ

- **LINQ** (Language Integrated Query)
- Integrovaný dotazovací jazyk, podobný jazyku SQL
- Slouží pro práci s daty v kolekcích
- Dotazy umožňují měnit strukturu dat, aniž by se změnil kód programu
- Umí zpracovávat data v XML souborech

### Operátory / metody

- Využívají se dotazové operátory = malá písmena, nevyužívá se lambda operátoru

```csharp
// Pomocí operátorů
var jmenaZak1 = from jmeno in z select jmeno.Jmeno;

// Zobrazení
foreach(string jmeno in jmenaZak1)
  Console.WriteLine(jmeno);
Console.WriteLine();
```

- Nebo metody = velká písmena, pro definici se využívá lambda operátor

```csharp
// PDotaz pro vybrání pouze jmén ze zákazníků
var jmenaZak = z.Select(zak => zak.Jmeno);

// Zobrazení
foreach(string jmeno in jmenaZak)
  Console.WriteLine(jmeno);
Console.WriteLine();
```

### Datový typ

- Datový typ dotazu je `var`, který si určí datový typ u překladu

### Jazyk LINQ

- LINQ pracuje s daty libovolné kolekce nebo polem
- Všechny kolekce se, kterými pracuje dědí z rozhraní `IEnumerable`
- Rozhraní umožňuje příkazy pro procházení kolekcí

### Enumerátor

- Je objekt, který vrací metodu `GetEnumerator` z kolekce
- Obsahuje referenci na daný prvek a pomocí metody `MoveNext` se přesune na další prvek kolekce
- Používá se kombinace `foreach` a cyklu `while`

```csharp
IEnumerator<int> enumerator2 = collection2.GetEnumerator();
while (enumerator2.MoveNext())
  Console.Write(enumerator2.Current);
```

### Postup práce:

- Vytvoříme si třídu s danými prvky, vlastnostmi, konstruktorem

```csharp
class Spolecnosti
{
  string spolecnost, mesto, zeme;

  #region properties
  public string Spolecnost { get => spolecnost; set => spolecnost = value; }
  public string Mesto { get => mesto; set => mesto = value; }
  public string Zeme { get => zeme; set => zeme = value; }

  #region construct
  public Spolecnosti(string s, string m, string z)
  #endregion
}
```

- Vytvoříme instanci konstruktoru

```csharp
Spolecnosti s1 = new Spolecnosti("Auto Moto", "Brno", "ČR");
Spolecnosti s2 = new Spolecnosti("Cyklo Svět", "Bratislava", "SK");
```

- Naplníme kolekci `LIST`

```csharp
List<Spolecnosti> s = new List<Spolecnosti>() { s1, s2 };
```

- Zobrazení kolekce

```csharp
foreach(Spolecnosti spol in s)
  Console.WriteLine(spol.Spolecnost + "\t" + spol.Mesto + "\t" + spol.Zeme);
Console.WriteLine();
```

## LINQ operace

- Výběr dat `SELECT`

```csharp
// Pomocí operátorů
var jmenaZak1 = from jmeno in z select jmeno.Jmeno;

// Zobrazení
foreach(string jmeno in jmenaZak1)
  Console.WriteLine();
Console.WriteLine();
```

- Výběr dvou a více prvků `SELECT`

```csharp
var celaJmenaZak1 = from jmeno in z select jmeno.Jmeno + "\t" + jmeno.Prijmeni;

foreach(string jmeno in celaJmenaZak)
  Console.WriteLine(jmeno);
Console.WriteLine();
```

- Filtrování dat `SELECT WHERE` - Při filtrování využíváme příkaz `SELECT` doplněný podmínkou `WHERE`

```csharp
var ceskeSpol = from spol in s where (spol.Zeme == "ČR") select spol.Spolecnost;

foreach(string nazev in ceskeSpol)
  Console.WriteLine(nazev);
Console.WriteLine();
```

- Řazení dat `ORDER BY`
  - Pro řazení dat použijeme příkaz `ORDER BY`
  - Řadit můžeme vzestupně `Ascending` nebo sestupně `Descending`

```csharp
var razeniSpolecnost2 = from spol in z orderby spol.Spolecnost descending select spol.Jmeno + "\t" + spol.Prijmeni + "\t" + spol.Spolecnost;

foreach(string zakaznici in razeniSpolecnost2)
  Console.WriteLine(zakaznici);
Console.WriteLine();
```

- Seskupování dat `GROUP BY`
  - Používá se příkaz `GROUP BY`
  - Pro výpis využití dvou cyklů `foreach`
  - Můžeme zde použít další metody: `MAX`, `MIN`, `AVERAGE`, `COUNT`

```csharp
var spolecnostSeskupeni1 = from spol in s group spol by spol.Zeme;

foreach(var seskup in spolecnostSeskupeni1)
{
  Console.WriteLine("země: {0}\tspolečnost: {1}", seskup.Key, seskup.Count());
  foreach(var spol in seskup)
    Console.WriteLine("\t{0}", spol.Spolecnost);
}

Console.WriteLine();
```

- Spojování dat
  - Umožňuje spojovat několik kolekcí přes jeden nebo více společných klíčových datových složek
  - Pomocí příkazu `JOIN`
  - Za on dosadíme prvek, ze kterého vycházíme => `from` a za `equals` prvek, kterým spojujeme => `join`

```csharp
var zakazniciZeme1 = from sp in s join a in z on sp.Spolecnost equals a.Spolecnost select new { a.Jmeno, a.Prijmeni, sp.Zeme };

foreach(var radek in zakazniciZeme1)
  Console.WriteLine(radek);
Console.WriteLine();
```

### Agregační funkce

- U `SELECTU` můžeme využít mnoho dalších metod a funkcí
- `MIN()` - vypíše nejmenší hodnotu
- `MAX()` – vypíše největší hodnotu
- `AVERAGE()` – spočítá průměr ze zadaných hodnot
- `COUNT()` – Spočítá počet prvků v kolekci
- `SUM()` – spočítá Součet daných prvků, použití u čísel
- `DISTINCT()` – odstranění duplicity v kolekci
- `FIRST()` – vrací první prvek
- `LAST()` – vrací poslední prvek
