# Pole

- Množina prvků se stejným datovým typem
- K jednotlivým prvkům pole přistupujeme pomocí indexů
- První prvek pole má index 0, poslední prvek má index n-1

## Deklarace

```csharp
datovy_typ[] nazev_pole;
```

- Deklarací vlastně vytvoříme odkaz
- Pokud chceme vytvořit místo v paměti musíme vytvořit instanci

```csharp
datovy_typ[] nazev_pole = new datovy_typ[pocet_prvku_pole];
```

- Počtem může být i proměnná, kterou vypočítáme

## Zapsání prvků do pole

### 1. Inicializace

```csharp
String[] predmety = new string[5]{"MAT", "ANJ", "CJL", "FYZ", "TEV"};
Console.WriteLine(predmety[3]); // vypížš "FYZ", protože je to prvek s indexem 3
String[] jmena = {"jan", "jirka", "dan"}; // další možnost inicializace
```

### 2. Zapsání pomocí indexů

```csharp
Byte[] znamky = new byte[4];
znamky[0] = 3;
znamky[1] = 2;
znamky[2] = 4;
znamky[3] = 1;
Console.WriteLine(znamky[1]); // vypíše se druhý prvek pole
```

### 3. Pomocí cyklu

```csharp
String[] zaci = new string[4];
for (int i = 0; i < 4; i++) {
	//
}
```

## Procházení pole

- Pro procházení se využívá cyklů:
  - **FOR** - musíme znát počet prvků pole
  - **FOREACH** - nemusíme si pamatovat index pole

```csharp
foreach (int n in numbers) {
	Console.WriteLine(n)
}
```

### Foreach

- Deklaruje iterační proměnnou, která automatický nabývá po průchodu cyklem hodnotu dalšího prvku pole.
- Iterační proměnnou můžeme deklarovat i pomoci var, pak si kompilátor C# odvodí datový typ z typu prvků pole.

### Nevhodný Foreach:

- Nechceme procházet celé pole (např. chceme zobrazit každý druhý prvek)
- Chceme procházet pole opačným směrem
- Potřebujeme znát aktuální hodnotu indexu
- Potřebujeme měnit hodnoty pole. Iterační proměnná je jen kopií prvků pole

## Zjištění délky pole

```csharp
Int[] nums = {5, 2, 69, 420};
Console.WriteLine(nums.length) // output 4
```

# Vícerozměrné pole

- Nejčastěji se využívá dvojrozměrné pole.
- Je to vlastně tabulka s určitým počtem řádků a sloupců.
- Z matematického pohledu, můžeme dvojrozměrné pole přirovnat k matici.

### Deklarace

```csharp
datovy_typ[,] nazev = new datovy_typ[x, y];
```

- x = počet sloupců
- y = počet řádků

### Naplnění pole

1. Pole můžeme naplnit bud postupně přiřazováním

```csharp
n[0, 0] = x;
n[0, 1] = y;
```

2. nebo použijeme cyklus FOR

### Výpis pole

- Pokud chceme zobrazit pouze určitý prvek pole, využijeme příkaz `Console.WriteLine();`
- Pokud chceme vypsat všechny prvky pole, využijeme cyklus FOR
- U dvojrozměrného pole použijeme 2 cykly FOR vnější (řádky) a vnitřní (sloupce)

# Metody pro práci s poli

- Můžeme používat statické metody třídy ARRAY nebo instanční metody.

## Třída Array

### Sort()

- Slouží pro setřídění pole vzestupně.

```csharp
// statické metody na poli třída Array
// Sort() - seřazení pole vzestupně
Array.Sort(nums);
```

### Reverse()

- Zobrazí pole od konce, pokud metodu aplikujeme na seřazené pole dostaneme pole seřazené sestupně

```csharp
// seřazení sestupně nejdřív seřadím vzestupně a pak po
// metodu Reverse() zobrazí pole od konce
Array.Reverse(nums);
```

### IndexOf

- Najde první pozici (číslo indexu) hledaného prvku pole, pokud nenajde nic, vrátí hodnotu **-1**.

```csharp
// pozice zadaného prvku INDEXOF
// pokud nenajde hledaný prvek do pozice se zapíše -1
```
