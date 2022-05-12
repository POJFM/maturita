# Tvorba webových stránek s formuláři a s přístupem k DB

- Tvorba formuláře v HTML – nejdůležitější prvky.
- Ošetření formuláře v PHP.
- Přístup k databázi v PHP.
- Použití SQL příkazů v PHP – výpis hodnot z databázové tabulky na základě zadané podmínky, zadání nového záznamu do tabulky.

<hr>

## Formulář v HTML

- Formuláře slouží ke komunikaci mezi uživatelem a serverem
- Formulář se skládá ze 3 částí:
  - **ELEMENT `<form>`** ► obsahuje URL adresu skriptu a metodu komunikace
  - **FORMULÁŘOVÉ POLE `<input>`** ► pole vyplňované uživatelem
  - **ODESÍLACÍ TLAČÍTKO** ► odesílá data z formuláře skriptu, který je zpracuje
- Základní tvar:

```html
<form metchod="POST" action="script.php">
  <label for="fname">First name:</label><br />
  <input type="text" id="fname" name="fname" /><br />
  <label for="lname">Last name:</label><br />
  <input type="text" id="lname" name="lname" />
</form>
```

### HTTP dotazovací metody

#### GET

- Odesílané informace se zobrazují v adresním řádku prohlížeče
- např. uživatel si může přidat do oblíbených položek výsledek hledání, vyhledávání
- informace nejsou soukromé

#### POST

- Umožnuje odesílat větší množství dat
- Odesílané informace se nezobrazují v adresním řádku prohlížeče (např. hesla)
- Komunikace s DB
- Vhodnejší pro většinu použití

### Formulářové prvky

- textová pole

```html
<input type="text" id="name" name="name" value="pepik" />
<!-- value - vychozí hodnota --->
```

- password pole

```html
<input type="password" />
```

- pole pro email, telefon, url

```html
<input type="email" />
<input type="tel" />
<input type="url" />
```

- přepínače

```html
<input type="radio" />
```

- zaškrtávací pole

```html
<input type="checkbox" />
```

- rozevírací seznamy (dropdown list)

```html
<label for="cars">Choose a car:</label>
<select id="cars" name="cars">
  <option value="volvo">Volvo</option>
  <option value="saab">Saab</option>
  <option value="fiat">Fiat</option>
  <option value="audi">Audi</option>
</select>
```

- textové oblasti

```html
<textarea name="message" rows="10" cols="30">
The cat was playing in the garden.
</textarea>
```

- tlačítka, submit

```html
<input type="button" id="ok" name="ok" /><input type="submit" id="ok" name="ok" />
```

### Ošetření formuláře v PHP

- V php se chceme vyvarovat jakémukoliv zobrazení kódu
- Ve formulářích může k takovému úniku dojít při špatně vyplnění formulářového pole
- Proto ošetřujeme podmínkou správné vyplnění
- Zamezíme tím kybernetickým útokům jako SQL Injection
- V příkladu: pokud je správně vyplněné pole „jmeno“ proběhnou příkazy 1, pokud není správně vyplněno tak proběhnou příkazy 2

```php
if (isset($_POST['jmeno'])) {
	echo('jmeno: ' . $_POST['jmeno']);
}
else {
	echo('Zadejte jméno.');
}
```

### Přístup k databázi v PHP

```php
$server = 'localhost';
$user = 'root';
$pswd = 'kokos';
$db = 'shop';

if (!mysql_connect($server, $user, $password)) {
	echo('DB je nedostupná');
}

if (!mysql_select_db($db)) {
	echo('nepodařilo se zvolit DB');
}

// nastavení znakové sady
mysql_query("SET NAMES 'utf8'");

// deklarace SQL dotazu
$query = "SELECT id, nazev, cena, kategorie FROM produkty";

// provedení SQL dotazu a uložení do pole $res
$res = mysql_query($query);

// vypsání všech záznamů z databáze bez tabulky
// mysql_fetch_array() prochází postupně jednotlivé prvky pole
while ($row = mysql_fetch_array($res)) {
	echo($row['id'] . ' ');
	echo($row['nazev'] . ' ');
	echo($row['cena'] . ' ');
	echo($row['kategorie'] . ' ');
}
// vypsání záznamů v tabulce
while ($row = mysql_fetch_array($res)) {
	echo('<tr>');
	echo('<td>' . $row['id'] . '</td>');
	echo('<td>' . $row['nazev'] . '</td>');
	echo('<td>' . $row['cena'] . '</td>');
	echo('<td>' . $row['kategorie'] . '</td>');
	echo('</tr>');
}

// přidání nového záznamu
$query = "INSERT INTO produkty (id, nazev, cena, kategorie) VALUES(NULL, 'auticko', 26, 1)";

// provedení SQL INSERT query
if (mysql_query($query))
	echo('zaznam pridan');
else
	echo('zaznam nepridan :(');

```
