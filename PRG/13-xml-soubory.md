# XML soubory

- Je to typ značkovacího jazyka, je samo popisovací
- Využívají se zde značky, tagy, elementy
- Další značkovací jazyky: `HTML`, `CSS`
- Soubor je textového typu podobný tabulce v excelu
- Vhodné pro ukládání malých databází

```xml
<!--
	Složení:
	Hlavička
-->
  <kořen>
    <prvek atribut>
      <textové elementy> </textový>
    </prvek atribut>
	</kořen>
<!-- /hlavička -->

<!-- například: -->

<?xml version="1.0" encoding="utf-8"?>
<sklad>
  <produkt ID="0">
    <nazevZbozi>Pantofle</nazevZbozi>
    <pocetKs>25</pocetKs>
    <cenaKs>419.99</cenaKs>
    <expirace>12/02/2020</expirace>
  </produkt>
  <produkt ID="1">
    <nazevZbozi>Bačkory</nazevZbozi>
    <pocetKs>45</pocetKs>
    <cenaKs>420</cenaKs>
    <expirace>02/03/2020</expirace>
  </produkt>
  <produkt ID="2">
    <nazevZbozi>Sandále</nazevZbozi>
    <pocetKs>66</pocetKs>
    <cenaKs>68.99</cenaKs>
    <expirace>21/01/2020</expirace>
  </produkt>
</sklad>

```

- XML soubory můžeme zapisovat pomocí `SAX, DOM, LINQ, Serializace, Deserializace`
- Nutné připojit knihovnu `using Systém.xml`

## SAX

- Zapisují se podobně jako metody `Stream`
- Jednotlivé elementy jdou za sebou
- Vytvoříme: třídu, kolekci, zápis do souboru, čtení ze souboru, výpis

```csharp
class Sklad
    {
        string nazevZbozi;
        int pocetKs, id;
        double cenaKs;
        DateTime expirace;

        //Vlastnosti
        public string NazevZbozi { get => nazevZbozi; set => nazevZbozi = value; }
        public int PocetKs { get => pocetKs; set => pocetKs = value; }
        public DateTime Expirace { get => expirace; set => expirace = value; }
        public int Id { get => id; set => id = value; }
        public double CenaKs { get => cenaKs; set => cenaKs = value; }

        //konstruktor
        public Sklad(int id, string nazevZbozi, int pocetKs, double cenaKs, DateTime expirace)
        {
            Id = id;
            NazevZbozi = nazevZbozi;
            PocetKs = pocetKs;
            CenaKs = cenaKs;
            Expirace = expirace;
        }
        public override string ToString()
        {
            return Id + " " + NazevZbozi + "  " + PocetKs + " " + CenaKs + "  " + Expirace;
        }
    }


// kolekce pro zapis
List<Sklad> skladWrite = new List<Sklad>();

// přidáme obsah do kolekce pro zapis
skladWrite.Add(new Sklad(0, "Pantofle", 25, 419.99, new DateTime(2020, 2, 12)));
skladWrite.Add(new Sklad(1, "Bačkory", 45, 420, new DateTime(2020, 3, 2)));
skladWrite.Add(new Sklad(2, "Sandále", 66, 68.99, new DateTime(2020, 1, 21)));
```

### Zápis do souboru XML

- Vytvořený soubor se uloží do `\složka programu\bin\Debug`

```csharp
// Nastavení writeru / značek pro odsazení
XmlWriterSettings nastaveni = new XmIWriterSettings();
nastaveni.Indent = true;

// Zápis uživatelů do xml instance zápisu:
static void writeFile(List<Sklad> sklad, XmlWriterSettings config)
    {
        using (XmlWriter zapis = XmlWriter.Create(@"pokus.xml", config))
        {
            //hlavička souboru resp začátek dokumentu
            zapis.WriteStartDocument();
            //otevřeme kořenový element
            zapis.WriteStartElement("sklad");
            //zapis jednotlivých elementů, procházím dcelou kolekci
            foreach (Sklad s in sklad)
            {
                zapis.WriteStartElement("produkt"); // začátek zápisu
                zapis.WriteAttributeString("ID", s.Id.ToString()); // ID je atributem
                zapis.WriteElementString("nazevZbozi", s.NazevZbozi);
                zapis.WriteElementString("pocetKs", s.PocetKs.ToString());
                zapis.WriteElementString("cenaKs", s.CenaKs.ToString());
                zapis.WriteElementString("expirace", s.Expirace.ToShortDateString());
                zapis.WriteEndElement(); // konec zápisu
            }
            zapis.WriteEndElement();
            zapis.WriteEndDocument(); // ukončení celého dokumentu
            zapis.Flush();
        }
    }
```

### Čtení ze souboru

```csharp
static List<Sklad> readFile(string path)
    {
        List <Sklad> sklad = new List<Sklad>();
        using (XmlReader reader = XmlReader.Create(@path))
        {
            // nadeklarujeme proměnné pro uložení vlastností
            int id = 0;
            string nazevZbozi = "";
            int pocetKs = 0;
            double cenaKs = 0;
            DateTime expirace = DateTime.Now; // nastavení aktualniho datumu for fun
            while (reader.Read()) {
                //čteme po uzlech (počáteční element, koncový element, text)
                if (reader.NodeType == XmlNodeType.Element)
                {
                    if (reader.Name == "produkt")
                        id = int.Parse(reader.GetAttribute("ID"));
                    else if (reader.Name == "nazevZbozi")
                        nazevZbozi = reader.ReadInnerXml();
                    else if (reader.Name == "pocetKs")
                        pocetKs = int.Parse(reader.ReadInnerXml());
                    else if (reader.Name == "cenaKs")
                        cenaKs = double.Parse(reader.ReadInnerXml());
                    else if (reader.Name == "expirace")
                        expirace = DateTime.Parse(reader.ReadInnerXml());
                }
                // načtení konce elementu přečetli jsme jednoho uživatele
                if (reader.NodeType == XmlNodeType.EndElement && reader.Name == "produkt")
                    sklad.Add(new Sklad(id, nazevZbozi, pocetKs, cenaKs, expirace));
                // načtení konce elementu přečetli jsme všechny uživatele
                if (reader.NodeType == XmlNodeType.EndElement && reader.Name == "sklad")
                    reader.Close();
            }
        }
        return sklad;
    }

  // přečíst XML
  List<Sklad> sklad = readFile("pokus.xml");
  
  //výpis načtených prvků kolekce
  Console.WriteLine("ID \t Celé jméno \t Věk \t Registrován");
  foreach (Sklad s in sklad)
  {
      Console.WriteLine(s.ToString());
  }
  Console.ReadLine();
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
