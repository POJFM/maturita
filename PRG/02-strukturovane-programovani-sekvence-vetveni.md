# Strukturované programování - sekvence, větvení

### Strukturované programování

- Princip je rozdělení složitých úloh na dílčí jednodušší úlohy, které se řeší samostatně
- Úkoly se následně spojí v jeden celek
- Patří zde: Sekvence, cykly, větvení, přepínače
- Příkazy se v metodě Main, vykonávají v počadí jakém jsou zadané

## Sekvence

- Nejjednodušší typ algoritmu
- Skládá se pouze z mezních značek, značka pro vstup avýstup dat a značek pro zpracování (přiřazení) dat
- Povolené operace: součet, rozdíl, součin, mocnina, OR, AND, negace
- Nepovolené operace: podíl, celočíselné dělení, odmocnina, cykly

### Vstupy / načtení

- `Console.ReadLine()` - přečtě řádek a vrací string, pro jiný datový typ musíme string přetypovat, např.:  `int num = int.Parse(Console.ReadLine())`
- `Console.ReadKey()` - čeká až se zmáčkne klávesa

### Různé formáty výpisu

```csharp
Console.Write("text") // ponechá kurzor na stejném řádku
Console.WriteLine("text") // přesune kurzor na nový řádek
Console.WriteLine("text \n text") // text za \n je na dalším řádku
Console.WriteLine("text \a text") // text za \n je na dalším řádku
Console.WriteLine("text \b text") // text za \n je na dalším řádku
Console.WriteLine("text \r text") // text za \n je na dalším řádku
Console.WriteLine("text \t text") // text za \n je na dalším řádku
Console.WriteLine("číslo {0} je o {1} větší než číslo {2}", a, b, c)
Console.WriteLine($"číslo {a} je o {b} větší než číslo {c}")
```

### Formátování čísla

Využijeme, když pro výpis používáme specifikací proměnných v složených závorkách. Za složenou závorku dáme dvojtečku a formátovací specifikaci.

```csharp
Console.WriteLine($"Měna: {n}:C")
```

| Formát             | Specifikace |
|--------------------|-------------|
| Měna               | C, Cn       |
| Desítková soustava | D, Dn       |
| Exponenciální      | E, En       |
| Pevná čárka        | F, Fn       |
| Obecný             | G, Gn       |
| Číslo              | N, Nn       |
| Procento           | P, Pn       |
| Hexadecimální      | X, Xn       |

## Větvení

- Větvení je alternativa rozhodování
- Využívá se pokud mají některé kroky být vynechané, nahrazené, přidané
- Ptáme se na otázky:
  - Co se stane, když platí podmínka
  - Co se stane, když podmínka neplatí
- První část je povinná, druhá nepovinná, (když platí provede se, neplatí nic se nestane)
- Podmínky obsahují relační operátory(==, !=, <,>…)
- Součástí mohou být i logické operátory AND(&&) OR(||)
- Pokud je příkaz 1 nebo 2 složený z více příkazů musí obsahovat { }

### Rozdělení větvení

**Úplné větvení**

- Má kroky pro kladnou i zápornou odpověď
- 
```csharp
if (podminka) {
    // do stuff if (podminka == true)
}
else {
    // do stuff if (podminka == false)
}
```

// img

**Neúplné větvení**

- Chybí krok pro kladnou nebo zápornou odpověd
  
```csharp
if (podminka) {
    // do stuff if (podminka == true)
}
```

// img

**Vnořené větvení**

- Má kroky pro kladnou i zápornou odpověď a ty jsou následně tvořeny dalším větvením
  
```csharp
if (podminka) {
    // do stuff if (podminka == true)
    ...
}
else {
    // do stuff if (podminka == false)
}
```

### Povolená operace
- součet (+)
- rozdíl (-)
- součin (*)
- mocnina SQR (^)
- logický součet (OR)
- logický součin (AND)
- negace (NOT)

### Nepovolené operace
- podíl (/) - nějaký
