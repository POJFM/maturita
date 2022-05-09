# Kolekce

- Kolekce použije tehdy, když do proměnné potřebujeme uložit větší množství dat a nevíme kolik prvku budeme mít.
- Jde vlastně o dynamické pole.
- Rozdělení kolekcí
  - Obecné
  - Generické

## Obecná kolekce

- Dědí z třídy Object a všem prvkům této kolekce se tento datový typ přiřadí.
- Pokud chceme získat prvek daného datového typu musíme jej přetypovat.
- Příkladem obecné kolekce je ArrayList
- Pro práci musíme mít připojený using System.Colections

### Nevýhody

- není možné provádět typovou kontrolu (při kompilaci nevíme jaký objekt jsme do kolekce vložili), na chybu se přijde až za běhu programu, když chceme načíst prvek z kolekce a přiřadit jej nějaké proměnné.
- Příklad: celočíselné proměnné přiřadíme des. Číslo, nastane výjimka InvalidCastException
- je zpomalení způsobené přetypováním

### Metody pracující s kolekcí Arraylist

- `Add(hodnota)` - přidá prvek na konec kolekce
- `Insert(pozice, hodnota)` - přidá prvek na zadanou pozici, ostatní prvky posune vpravo. pokud zadame větši index než je aktuáiní počet prvků objeví se chybové hlášeni `Argument OutOfRoange Exception`.
- `Remove(hodnota)` - vyjme zadanou hodnotu z kolekce
- `RemoveAt(index)` - vyjme prvek na zadaném indexu
- `Clear()` - odebere všechny prviy z kolekce
- `Contains(hodnota)` - zjisti, zda kolekce obsahuje zadanou hodnotu - pokud ano vraci `1` jinak `O`
- `Capacity` - velikost kolekce
- `Count` - aktuálni počet prvkù
- `Sort()` - setřídí prvky
- `Reverse()` - převrátí pole 1. prvek bude poslední a naopak
- `BinarySearch()` - vyhledávání prvků v kolekci (ypiše pozici hledaného prvku)
- `RemoveRange()` - odstrani oblast prvkú
- Ke všem prvkům obecné kolekce přistupujeme stejně jako k prvkům pole přes index, ten začiná vždy `0`.
- Pro výpis prvků použijeme cyklus `FOR` nebo `FOREACH`

## Generická kolekce

- Generická proměnná může mít Libovolný datový typ, který je definován pro danou třídu.
- Třída obsahuje ve svojí definici generický parametr, který se zadává do špičatých závorek (`<>`), generických parametrů může být několik
- Může obsahovat proměnné, konstruktory, metody
- V `Main` potom vytváříme instanci konstruktoru s parametry

## LIST

- Je to generická kolekce
- Během programu můžeme přidávat nebo mazat prvky
- Rozdělujeme dva typy seznamu:

### LIST[] (Seznam s polem)

- Vytvoříme si pole s určitým výčtem prvků
- Prvky se vkládají přes indexy
- Nevýhoda pomalejší, zabírá více paměti
- Nejpoužívanější kolekce

```csharp
//vytvoření kolekce
List<Zavodnik> zavod = new List<Zavodnik>()
{
  //Naplnění kolekce prvky
  new Zavodnik (1, "Kristýna", "Hezká", 17, 42),
  new Zavodnik (2, "Beata", "Frydecká", 18, 69),
  new Zavodnik (4, "Ondra", "Debil", 21, 118),
  new Zavodnik (6, "Dalibor", "Borec", 89,423),
  new Zavodnik (11, "Matëj", "polský", 33,88)
}; //střednik

Console.WriteLine("Zobrazení kolekce závod: ");
// zobrazení kolekce
foreach (var zobraz in zavod)
  Console.WriteLine(zobraz);
```

### Metody na třídě LIST

- `Capacity` - zjistí kapacitu kolekce
- `Count` - zjistí aktuální počet prvků v kolekci
- `Add(hodnota)` - přidá prvek do kolekce
- `Insert (index, hodnota)` - přidá prvek na zadaný index, ostatní prvky posune vpravo
- `IndexOf(hodnota)` - zjisti index, na kterém se nacházi hledaná hodnota
- `BinarySearch(hodnota)` - zjisti index hledané hodnoty ve seřazené kolekci
- `Find(predikát > podmínka)` - vyhledá první hodnotu odpovidající podmínce. Využvá lambda operátor `=>`
- `FindAll(predikát => podmínka)` - vyhledá všechny prvky odpovidajicí podmínce a uloži je do nové kolekce
- `Exists(predikát => podmínka)` - zjistí, zda v kolekci je prvek odpovidající podmínce. Vrací true nebo false
- `Sort()` - seřazení kolekce
- `Reverse()` - obrácení kolekce
- `AddRange(kolekce2.ToArray())`-spojí dvě kolekce, nutno převést na pole přes `ToArray`
- `CopyTo(pole)` - zkopírování kolekce do pole
- `Remove(hodnota)` - vymaže zadanou hodnotu
- `RemoveAt(index)` - vymaže hodnotu na zadaném indexu
- `RemoveAll(predikát > podminka)` - vymaže prvky odpovidajicí podmince
- `RemoveRange(index, počet prvků)` - vymaže zadaný počet prvků od zadaného indexu
- `Clear()` - vymaže celou kolekci

### Linked LIST (Spojový seznam)

- Prvky ve spojovém seznamu nejsou uloženy za sebou, ale jsou rozházené po paměti
- Neodkazujeme na něj pomocí indexu
- Jednosměrný – prvek odkazuje na následující
- Obousměrný – prvky na sebe odkazují navzájem
- Prvky v kolekce jsou obaleny uzlem

<br>

- `AddAfter(uzel, hodnota)` - přidá prvek za daný prvek
- `AddBefore(uzel, hodnota)` - přidá prvek před daný prvek
- `AddFirst(hodnota)` - přidá prvek na začátek
- `AddLast(hodnota)` - přidá prvek na konec
- `First` - vlastnost, která vrátí první prvek
- `Last` - vlastnost, která vrátí poslední prvek
- `RemoveFirst` - vymaže první prvek
- `RemoveLast` - vymaže poslední prvek

## Množina

- Ukládají prvky v kolekci hashováním.
- Zajistí, že prvek je v kolekci pouze jednou.
- Základní třída `HashSet`

```csharp
HashSet<uchazeci> Anj = new HashSet<uchazeci>();
```

## Fronta

- Prvky se v programu řadí do jak do fronty v obchodě
- Když se přidá nový prvek zařadí se nakonec
- Prvky se odebírají od prvního
- Přidává se prvek - `Enqueue`
- Odebírá se prvek – `Dequeue`

```csharp
Queue<zakaznik> zakaznici = new Queue<zakaznik>();
```

## Zásobník

- Dočasné ukládání dat
- `Push()` - přidá do zásobníku
- `Pop()` - odebere ze zásobníku

```csharp
//Nastavení zásobniku
Stack<bod> poloha = new Stack<bod>();
```

- Pomocí kláves můžeme v zásobníku pohybovat prvkem
