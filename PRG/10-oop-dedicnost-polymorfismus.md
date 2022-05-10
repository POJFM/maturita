# OOP dědičnost, polymorfismus

- Dědičnost (umožňuje vytvořit nové objekty z původních, nové objekty dědí vlastnosti)
- **Dědičnost** – objekty získávají vlastnosti z jiných objektů
- Společné vlastnosti a metody se definují v základní třídě
- Ve zbylých třídách jsou jen specifické vlastnosti a metody
- Vlastnosti, které dědíme nemohou mít práva `private` musí být vždy `public` / `protected`

<br>

<img src="./img/oop-trida.png" style="width:500px">

<br>

- **Polymorfismus** (umožňuje vytvořit jednu metodu pro více objektů, ale pro každý objekt se bude chovat jinak)

## Dědění třídy

- Opět musíme nadefinovat třídu jako `public`

```csharp
public class Osobni : Vozidlo
{
  // Tělo funkce
}
```

## Dědění členů

- Konstruktor, dědění dat členů z vozidla `pk` a `del` dědění `:base(parametr, parametr)`

```csharp
public Osobni(int pm, int pk, float del)
: base(pk, del)
{
  this.pocet_mist = pm;
}
```

- Ve třídě vozidlo nadeklarujeme hodnoty, vytvoříme konstruktor, vlastnosti, metodu pro zobrazení
- Metoda `Zobraz()` je použitá ve všech třídách, ale v každé zobrazuje něco jiného => metoda je polymorfní. Polymorfní metody se u předka označují slovem `virtual` a u potomka slovem `override`.

```csharp
public virtual void Zobraz()
{
  Console.WriteLine("Počet kol je: {0}\ndélka auta je: {1} metrů", Pocet_kol, Delka);
}
```

```csharp
// Metoda dědí původní metodu  + dopíše počet míst
// Metoda přepisuje původní metodu - ta je označena jako virtual
public override void Zobraz()
{
  base.Zobraz();
  Console.WriteLine("Počet míst: {0}", Pocet_mist);
}
```
