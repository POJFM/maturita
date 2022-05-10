# ADO.NET - připojený režim

- Pracuje se daty přímo na databázovém serveru
- Vytvoříme WA form pro zadání dat
- Musíme připojit knihovnu klienta using Systém.Data.SqlClient

**Připojovací řetězec** - je vlastnost, kde je uvedená cesta a slouží pro připojení Databáze k aplikaci

Připojení děláme přes server explorer, klikneme na zvolenou databázi a cestu v Conection string zkoprírujeme do programu

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

## Mazání záznamu

```csharp
private void BtnVymaz_click(object sender, EventArgs e)
{
	string prijmeniA = TxtPrijmeni.Text;
	// Do textu příkazu nebudeme vkládat proměnné, ale parametry, na které se budem následně odkazovat
	// Parametry použivame aby byla DB bezpečnější
	// Pokud vkládáme přimo proměnné může do textového pole uživatel vložit SQL přikaz a narušit nebo zrušit DB
	// Paremetr začíná vždy @
	string textprikazu = "delete from Kniha where Autor_prijmeni = @Autor_prijmeni"

	// Instance (objekt) příkazu
	SqlCommand prikaz = new SqlCommand(textPrikazu);

	// Pomocí commandu přídam/přiradim jednotlivým parametrům konkrétní hodnotu
	// Parametru @Autor_jmeno přiřadím hodnotu z proměnné jmenoA
	prikaz.Parameters.AddWithvalue("@Autor_prijmeni", prijmeniA);

	// Objekt pro připojení
	Sqlconnection connect = new Sqlconnection(pripojivaciRetezec);

	// Otevření připojení
	connect.Open();
	// Přidání připojení k přikazu
	prikaz.Connection = connect; // Přes vlastnost Connection přiřadím do přikazu připojení
	// Provedení přikazu
	prikaz.ExecuteNonQuery();
	connect.close();
}
```

## Transakce

- Umožňuje provést několik dotazů zároveň a buď je provedou všechny nebo ani jeden

### Mazání využitím transakcí

```csharp
// Vytvoříme instanci pro transakce
SqlTransaction transakce = connect.BeginTransaction();
// Procházim celou kolekciseznamID a postuně mažu, nejdřiv v tabulce pujcky a pak kniha
foreach (int s in seznamId)
{
	// V tabulce pujcky
	textPrikazu = "delete from Pujcky where Idkniha=@IdKniha ";
	prikaz = new SqlCommand(textPrikazu, connect);
	prikaz.Parameters.AddWithValue( "@IdKniha", s);
	prikaz.Transaction = transakce;
	prikaz.ExecuteNonQuery ()
	// V kniha
	textPrikazu = "delete from Kniha where Id=@Id ";
	prikaz = new SqlCommand (textPrikazu, connect);
	prikaz.Parameters.AddWithValue ( "@Id" , s);
	prikaz.Transaction = transakce;
	prikaz.ExecuteNonQuery();
}
transakce.Commit();
connect.Close();
MessageBox.Show("bylo smazano: " + seznamId.Count.ToString());
```

## Update záznamu

```csharp
private void BtnAktualizuj_click(object sender, EventArgs e)
{
	// Vytvoření připojení
	SqlConnection connect = new SqlConnection (PripojovaciRetezec);
	string textPrikazu = "update Kniha set PocetKs=5 where pocetKs<=2";
	SqlCommand prikaz = new SqlCommand(textPrikazu, connect);
	connect.Open();
	prikaz.ExecuteNonQuery();
	connect.Close();
}
```
