# XML soubory

- Je to typ značkovacího jazyka, je samo popisovací
- Využívají se zde značky, tagy, elementy
- Další značkovací jazyky: `HTML`, `CSS`
- Soubor je textového typu podobný tabulce v excelu
- Vhodné pro ukládání malých databází

```
Složení:
Hlavička
  <kořen>
    <prvek atribut>
      <textové elementy> </textový>
    </prvek atribut>
	</kořen>
/hlavička
```

- XML soubory můžeme zapisovat pomocí `SAX, DOM, LINQ, Serializace, Deserializace`
- Nutné připojit knihovnu `using Systém.xml`

## SAX

- Zapisují se podobně jako metody `Stream`
- Jednotlivé elementy jdou za sebou
- Vytvoříme: třídu, kolekci, zápis do souboru, čtení ze souboru, výpis

```csharp
class Uzivatele
{
  string celeJmeno;
  int vek;
  DateTime registrovan;

  //vlastnosti
  public string CeleJmeno { get => celeJmeno; set => celeJmeno = value; }
  public int Vek { get => vek; set => vek = value; }
  public DateTime Registrovan { get => registrovan; set => registrovan = value; }

  //konstruktor
  public Uzivatele(string j, int v, DateTime r)
  {
    CeleJmeno = j;
    Vek = v;
    Registrovan = r;
  }

  public override string ToString()
  {
    return CeleJmeno + " " + vek + " " +registrovan;
  }
}

//vytvoření kolekce
List<uzivatele> uzivatel = new List<Uzivatele>();

//přidáme uživatele do kolekce
uzivatel.Add (new Uzivatele ("Jan Novák", 25, new DateTime (2020, 2, 12)));
uzivatel.Add (new Uzivatele ("Iveta Modrá", 45, new DateTime (2020, 3, 2)));
uzivatel.Add (new Uzivatele ("Ivan Obrovský", 66, new DateTime (2020, 1, 21)));
```

### Zápis do souboru XML

- Vytvořený soubor se uloží do `\složka programu\bin\Debug`

```csharp
// Nastavení writeru / značek pro odsazení
XmlWriterSettings nastaveni = new XmIWriterSettings();
nastaveni.Indent = true;

// Zápis uživatelů do xml instance zápisu:
using (XmlWriter zapis = XmlWriter.Create (@"pokus.xml", nastaveni))
{
  // Hlavička souboru resp začátek dokumentu
  zapis.WriteStartDocument();

  // Otevřeme kořenový element
  zapis.WriteStartElement("uzivatele");

  // Zápis jednotlivých elementů, procházím dcelou kolekci
  foreach (Uzivatele u in uzivatel)
  {
    zapis.WriteStartElement("uzivatel"); // Začátek zápisu
    zapis.WriteAttributeString("ID", u.Id.ToString()); // ID je atributem
    zapis.WriteElementstring("vek", u.Vek.ToString(O));
    zapis.WriteElementSstring("jmeno", u.CeleJmeno);
    zapis.WriteElementString("registrovan ", u.Registrovan. ToShortDateStrings());
    zapis.WriteEndElement(); // Konec zápisu
  }

  zapis.WriteEndElement();
  zapis.WriteEndDocumernt (); // Ukončení celého dokumentu
  zapis.Flush();
}
```

### Čtení ze souboru

```csharp
using (XmlReader cteni = XmlReader.Create(@"pokus.xml"))
{
  // Nadefinujeme proměnné pro uložení vlastností
  int id = 0, vek 0;
  string jmeno = "", element = "";
  DateTime registrovan = DateTime.Now; // Nastavení aktualniho datumu

  // Čteme po uzlech (počáteční element, koncový element, text)
  if (cteni.NodeType == XmlNodeType.Element)
  {
    element = cteni.Name; // Přiřazení názvu elemtu, který jsme přečetli
    if (element == "uzivatel")
      id int.Parse(cteni.GetAttribute("ID"));

    // Načitam hodnoty v elementu
    else if (cteni.NodeType == XmlNodeType.Text)
    {
      switch (element)
      {
        case "vek":
          vek = int.Parse(cteni.Value); // Nutné přetypovat
          break;
        case "jmeno" :
          jmeno = cteni.Value;
          break;
        case "registrovan":
          registrovan = DateTime.Parse(cteni.Value);
          break;
      }
    }
  }

  // Výpis načtených prvků do konzole
  Console.WriteLine("ID \t celé jméno \t Věk \t Registrován");

  foreach (Uzivatele u in uzivatel)
  {
    Console.WriteLine(u.Id + "t" + u.CeleJmeno + "it" + u.Vek + "\t" + u.Registrovan.ToShortDateString());
  }

  Console.ReadLine();
}
```

## DOM (Document Object Model)

- Objektový přístup
- Vytvořím instanci dokumentu a do něj přes `AppendChild(prvek)` vložím jednotlivé prvky
- Funguje podobně jako SAX má trošku jinou syntaxi
- Vytvoříme třídu, kolekci, zápis do souboru, čtení ze souboru

## LINQ (Language Integrated Query)

- Objektový přístup
- Nutno připojit knihovnu `using Systém.xml.LINQ`
- Soubor vytvářím při deklaraci do konstuktoru z třídy `XDocument`
- Hlavička je `XDeclaration` kde zadáváme kódování, vezri
- Obsah je `XElement` (Nazev elementu, proměnná z třídy)
- Cyklus `FOREACH`

## Serializace a Deserializace

- Vhodné pro WA
- Pro třídu, kterou serializujeme musíme připojit knihovny `using Systém.IO` a `using System.Xml.Serialization`
- Vytvoříme třídu, kolekci, zápis pomocí serializace
- Soubory můžeme vypisovat, přidávat pomocí listboxu a tlačítek
