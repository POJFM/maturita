# DLL knihovny

- Knihovny metod DLL (Dynamic Link Library), které si můžeme sami nadefinovat pro další využití v aplikaci

## Vytvoření knihovny DLL

- Vytvoříme je přes šablonu `class library` (knihovna tříd)
- Třída obsahuje pouze metody instance
- Spouštím `F6`, nebo buildnu manuálně přes `Build > Build solution`. Do složky debug se poté vytvoří soubor DLL
- V aplikaci, ve které chci knihovnu použít `References > PTM > AdapterReference` a vyberu knihovnu
- Poté připojím jmenný prostor DLL a pokud tam jsou instanční metody vytvořit instanci

## DLL Knihovna

```csharp
namespace UtilityLibraries;

public static class StringLibrary
{
  public static bool StartsWithUpper(this string? str)
  {
    if (string.IsNullOrWhiteSpace(str))
      return false;

    char ch = str[0];
    return char.IsUpper(ch);
  }
}
```

## Program

```csharp
// připojení knihovny
using UtilityLibraries;

class Program
{
  static void Main(string[] args)
  {
  	int row = 0;

    do
    {
      if (row == 0 || row >= 25)
        ResetConsole();

      string? input = Console.ReadLine();
      if (string.IsNullOrEmpty(input)) break;
        Console.WriteLine($"Input: {input}");
      Console.WriteLine("Begins with uppercase? " + $"{(input.StartsWithUpper() ? "Yes" : "No")}");
      Console.WriteLine();
      row += 4;
    } while (true);
      return;

    // Declare a ResetConsole local method
    void ResetConsole()
    {
      if (row > 0)
      {
        Console.WriteLine("Press any key to continue...");
        Console.ReadKey();
      }
      Console.Clear();
      Console.WriteLine($"{Environment.NewLine}Press <Enter> only to exit; otherwise, enter a string and press <Enter>:{Environment.NewLine}");
      row = 3;
    }
  }
}
```
