# SQL DCL grat, revoke

<br>

<img src="./img/vytvoreni-vypis-uzivatele.png" style="width:600px">

<br>

## Typy uživatelů

<br>

<img src="./img/typy-uzivatele.png" style="width:400px">

<br>

## Přidělení práv

- Uživatelské účty jsou uloženy obvykle v systémových tabulkách.
- Každý SŘBD používá vlastní systém uložení uživatelských dat.
- Dva základní příkazy ke správě účtů:
  - `GRANT` - vytváří účty a specifikuje jejich práva.
  - `REVOKE` - odvolává práva k existujícím účtům.
- Příkaz na kontrolu oprávnění:
  - `SHOW GRANTS FOR 'uzivate1'@'host';`
  - `SHOW PRIVILEGES` - zobrazí oprávnění, která lze udělovat včetně kontextu.

### Přidělení všech práv vytvořenému uživateli

<br>

<img src="./img/grant-all-privileges.png" style="width:500px">

<br>

## Základní typy oprávnění

<br>

<img src="./img/grant.png" style="width:500px">

<br>

<br>

<img src="./img/grant-revoke.png" style="width:500px">

<br>

<br>

<img src="./img/grant-select.png" style="width:500px">

<br>

<br>

<img src="./img/grant-option.png" style="width:500px">

<br>

<br>

<img src="./img/pass-bezpecnost.png" style="width:500px">

<br>