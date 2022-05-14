# OOP abstraktní třída rozhraní

## Rozhraní (Interface)

- kompletně abstraktní třída
- může obsahovat pouze abstraktní metody a vlastnosti (nemají tělo `{}`)
- Rozhraní umožňuje instancí nastavit přístup pouze některým metodám = to je těm, které jsou v daném rozhraní definované
- `C#` neumožňuje vícenásobné dědění z tříd, může ale vícenásobně dědit z rozhraní.
- Rozhraní obsahuje pouze hlavičky metody, vlastnosti nebo indexerů, které chci instancí přidělit
- Rozhraní můžeme použit při tvorbě instance začíná vždy `Inazev`
- Třída z rozhraní v `C#` dědí pomocí `:`
- Přes rozhraní můžeme vytvořit instanci

### Instance rozhraní:

`Irozhrani i1=new KonstruktorTridy(parametry);`

- Taková instance má pak přístup pouze k metodám, které jsou definované v rozhraní na rozdíl od instanci vytvořených přes třídu `Třída t1= new KonstruktorTridy(parametre)`, které mají přístup ke všem metodám v dané třídě.
- Tzn. rozhraní může instanci omezovat v přístupu ke všem metodám třídy.
- Vytvoříme hlavní třídu a Jednotlivé rozhraní, které dědí ze třídy, vlastnosti, konstruktor pro zaměstnance

```csharp
class Skola : IZak, IZamestnanec
{
  //deklarace
  string jmeno, prijmeni, pozice, trida;
  int plat, zn1, zn2, zn3;

  //vytvoření vlastností:
  public string Jmeno { get => jmeno; set => jmeno = value;}
  public string Prijmeni {get => prijmeni; set => prijmeni = value; }
  public string Pozice { get => pozice; set => pozice = value; }
  public string Trida { get => trida; set => trida = value; }

  public int Plat { get => plat; set => plat = value;}
  public int Zn2 { get => zn2; set => zn2 = value; }
  public int Zn1 { get => znl; set => znl = value; }
  public int Zn3 { get => zn3; set => zn3 = value; }

  //vytvoření konstruktoru pro zaměstnance školy
  public Skola (string jm, string prj, string poz, int pl)
  {
    this.Jmeno = jm;
    this.Prijmeni = prj;
    this.Pozice = poz;
    this.Plat = pl;
  }
}
```

- Vytvoříme metodu pro výpis zaměstnance + navýšení platu

```csharp

public void vypisZamestnanec()
{
  Console.WriteLine("PÈijmení zaméstnance (0) \n Jméno zamėstnance - (1  \n Pozice (2) In Plat - (3}", Jmeno, Prijmeni, Pozice, Plat);
  Console.WriteLine();
  Console.WriteLine("************************************************");
}

public int Zvyseni(int castka)
{
  return Plat + castka;
}
```

- Vytvoříme metody v rozhraní, které chceme používat při výpisu zaměstnance

```csharp
interface IZamestnanec
{
  //nastavení omezujicích hodnot pro Zaměstnance
  void VypisZamestnanec();

  int Zvyseni(int castka);
}

// Omezený výpis => Zaměstnanci nebudu vypisovat známky, třídu... Ani nebudu používat metodu Prumer na výpočet průměrné mzdy. Naopak potřebuji výpis pro zaměstnance s polemi plat a pozice + metodu navýšení platu.
IZamestnanec zam1 = new Skola("Kristýna", "Světlá", "Profesorka", 45000);
zam1.VypisZamestnanec();
Console.WriteLine(Zvyseni(1000000));
```

## Abstraktní třída

- Je nejobecnější třída, která obsahuje datové členy, konstruktor, vlastnosti, nevytváří se z ní instance.
- Metody, které jsou společné ve všech potomcích se pak označují jako abstraktní a skládají se pouze z hlavičky metody.
- Ve zděděné třídě se metoda označuje jako přepsaná.
- Účelem abstraktní třídy je poskytnout společnou definici základní třídy, kterou může sdílet více odvozených tříd.

```csharp
//Nutné nadefinovat třidu jako public abstract
public abstract class Vozidlo
{
  // Třída vozidlo bude obsahovat: počet kol, délku, meotodu pro zobrazení
  //Deklarace
  int pocet_kol;
  float delka;

  //konstruktor
  public Vozidlo (int pk, float del)
  {
    this.pocet_kol = pk;
    this.delka = del;
  }

  // Vlastnosti vytvořenné přes refraktoring
  public int Pocet_kol { get => pocet_kol; set => pocet_kol = value; }
  public float Delka { get => delka; set => delka = value; }
  
  //Abstraktní metoda neobsahuje žádné parametry
  public abstract void Zobraz();
}
```
