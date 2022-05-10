# OOP základní pojmy

## Třída

- Je datový typ pomoci, kterého vytváříme objekty
- Objekt je potom instancí třídy
- Třída má své členy, které jsou v ní deklarované, nebo zděděné

### Objektově orientované programování

- Soubor doporučení, jak má program vypadat
- Řídíme zde tok událostí
- Charakterizují jej tři základní vlastnosti:
  - **Zapouzdření** (využívá se datový typ objekt, který je obalen řídícími strukturami metodami)
  - **Dědičnost** (umožňuje vytvořit nové objekty z původních, nové objekty dědí vlastnosti)
  - **Polymorfismus** ( umožňuje vytvořit jednu metodu pro více objektů, ale pro každý objekt se bude chovat jinak)

### Rozdělení členů

- Datové
- Funkční

## Datové členy

- Ukládají data specifické pro danou třídu
- Ze třídy se vytváří objekty, které si pamatují svůj stav např. objekt ,,pacient,, má svoje jméno, příjmení, stav… tyto informace jsou uloženy v datových členech

### Rozdělení datových členů

#### Datové položky

- Je to každá proměnná deklarovaná ve třídě
  - `public` - přístup zvenčí měnit zvenčí
  - `private` - platné pouze pro danou třídu a zvenčí nelze k nim přistoupit (k proměnným atd..)
  - `protected` - dědíme je, chráněné, v základní třídě a dědíme je do podřízených třid (odkaz pomoci base)

#### Události

- Každý objekt může vyvolat nějakou událost
- Například kliknutím na tlačítko se něco provede

## Funkční členy

### Metody

- Metoda slouží k tomu abychom mohli měnit stav objektu, nebo podávali informace o stavu objektu.
- Je to souhrnný název pro funkce a procedury.
- Metoda je jakási černá skříňka, která má vstupy a výstupy a okolní programy o nich vědí, ale nepotřebují vědět co je uvnitř.
- Metodu můžeme kdykoliv vylepšit, změnit a pro okolní programy se nic nemění, pokud nezměníme signatura. Použití metody v hlavním programu označujeme jako volání metody.

### Rozdělení metod:

#### Statické

- Není potřeba vytvářet instanci třídy (nepracuje s objektem) a volá se v hlavním programu přes třídu

```csharp
public static /*návratový datový typ*/ NázevMetody (/*seznám formálních
parametrů*/)
{
  // Tělo metody
}
```

- **Návratový datový typ** - dat. typ výsledku, který metody vrací
- **Název metody** - začíná vždy velkým písmenem
- **Formální parametry** - jsou lokální proměnné, do kterých se vkládají hodnoty skutečných proměnných při volání funkce.
- **Tělo metody** - tady se provádí vlastní výpočet, výsledek se vrací klíčovým slovem `return`

#### Instanční

- Vyžaduje vytvoření instance objektu pomoci, kterého je pak volána
- Nejčastěji typu `void`

### Konstruktory

- Každý objekt by měl být v daném okamžiku ve správném stavu, proměnné by měly nabývat správné hodnoty
- Tento správný stav by měl být zachován ihned po vytvoření instance => konstruktor.
- Je to vlastně metoda volána při vytváření nové instance dané třídy
- Vždy `public`, nemá datový typ, název je totožný s názvem třídy `this` => to, co je nedeklarované v části datových členů

### Druhy konstruktorû

- **Bez parametru**
  - Hned přidám proměnné
  - Není nic v závorce konstruktoru
- **S parametrem**
  - Do závorky parametry s dat typy nemusí mít stejné jméno jak ve třídě
  - `this` odkazuje na proměnné datových členů
  - Vlevo datové členy, vpravo konstruktorové
- **Přetížený konstruktor**
  - Více konstruktorů v jedné třídě

### Vlastnosti

- Data v objektu by měly být privatní a přistupovat k nim, by se mělo přes veřejné funkční členy
- Vlastnosti (`properties`) se zabývají zpracování prvních dvou typů zpráv.
- Pokud nebudeme používat vlastnosti, tak dotazovací zpráva se implementuje pomocí metody `Get` a informační zpráva se implementuje pomoci metody `Set`
- `get` - pro čtení
- `set` - pro nastavování
- V OOP komunikujeme s objekty prostřednictvím zpráv, které mohou být:
- **Informační (informative message)** - informuje o tom, že se někde v systému změnili údaje o objektu a objekt by se měl aktualizovat.
- **Dotazovací (interrogative message)** - dotazuje se objektu na jeho stav, protože to např. potřebuje zobrazit v dialogovém okně
- **Přikazovací (imperative message)** - říka se jím i akční, požadují po objektu nějakou akci, např. výpočet, analýzu apod.
