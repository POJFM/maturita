# ADO.NET - připojený režim

- Pracuje se daty přímo na databázovém serveru
- Vytvoříme WA form pro zadání dat
- Musíme připojit knihovnu klienta using Systém.Data.SqlClient
- **Transakce** – provádí několik dotazů zároveň, provedou se všechny nebo žádný

**Připojovací řetězec** - je vlastnost, kde je uvedená cesta a slouží pro připojení Databáze k aplikaci

Připojení děláme přes server explorer, klikneme na zvolenou databázi a cestu v Conection string zkoprírujeme do programu

```csharp
// code
```

## Vkládání záznamů

- Dvěma různými způsoby bezparametricky a parametricky
- Parametrický způsob je lepší způsob, bezpečnější, zabránění vložení SQL kódu
- Vytvoříme proměnné do a propojíme s textboxem

```csharp
private void button1_Click(object sender, EventArgs e) {
	string prijmeni = txt_prijmeni.Text;
	string jmeno = txt_jmeno.Text;
	string mesto = txt_mesto.Text;
}
```

- Vložíme SQL příkaz pro vložení

```csharp
// text query
// místo hodnoty, nebo proměnné zadáme parametr, který začíná @
string query = "INSERT INTO Zakaznici(Prijmeni, Jmeno, Mesto, ...)values(@Prijmeni, @Jmeno, @Mesto, ...)";
```

- Vytvoříme instanci příkazu SQL

```csharp
SqlCommand prikaz = new SqlCommand(textPrikazu);
```

- Přidáme parametry

```csharp
prikaz.Parameters.AddwithValue("@Prijmeni", prijmeni);
prikaz.Parameters.AddwithValue("@jmeno" , jmeno);
prikaz.Parameters.AddwithValue("@mesto" , mesto);
prikaz.Parameters.AddwithValue("@mail", mail);
prikaz.Parameters.AddwithValue("@telefon", telefon);
prikaz.Parameters.AdduithValue("@kolo", kolo);
```

- Připojíme databázi pomocí sql connection, propojíme s řetězcem pro připojení

```csharp
SqlConnection pripojeni = new SqlConnection(Propojeni)
```

- Otevřeme připojení, přidání připojení k příkazu, provedení příkazu, ukončení

```csharp
pripojeni.Open();

// Přidání připojení k příkazu
prikaz.Connection = pripojeni;

// Provedení příkazu
prikaz.ExecuteNonQuery();

// Zavření připojení
pripojeni.Close();
```
- `ExecuteNonQuery` – spuštění dotazu typu delete, insert, nemá žádnou hodnotu