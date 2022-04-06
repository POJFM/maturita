# Uživatelé a skupiny
- Systémové soubory a jejich struktura
- Superuživatel root
- Základní příkazy pro práci s uživateli
- Změna hesla
- Profil uživatele
- Přidání, odebrání editace uživatelů a uživatelských skupin
- Nahrazení identity
- Delegování práv
    - Instalace nástroje
    - Konfigurace - uživatelé, skupiny, hosté, příkazy
    - Aliasy
- Pseudouživatelé

## Systémové soubory a jejich struktura
- `/etc/passwd`
    - Informace o uživatelích
    - `Uživatelské_jméno:heslo:UseID:GroupID(základní skupina uživatele):GECOS(info o uživateli):user_home:shell`
    - Když je u hesla `*` - heslo je zablokované
    - Když je u hesla `X` – heslo je stínové, hledá se v souboru etc/shadow
    - ID 0 = root. ID 1- 1000 systémoví uživatelé, 1000 – 65533 normální uživatelé
- `/etc/group`
    - Seznam skupin, kteří uživatelé se nachází v jakých skupinách
- `/etc/gshadow`
    - Heslo pro skupiny uživatelů
- `/etc/shadow`
    - `uživatel:heslo:parametry hesla` (kdy vyprší apod.)
    - Heslo je zahešované
- Parametry:
    - Poslední změna hesla: Days since Jan 1, 1970 that password was last changed
    - Minimum dnů, které musí uplynout pro možnost další změny hesla         
    - Maximum dnů, po které je heslo platné, než se bude muset změnit
    - Počet dnů před tím než bude uživatel varován, že mu končí heslo
    - Počet dnů kdy je účet po vypršení hesla nedostupný
## Superuživatel root
- **UID = 0**
- Tento správce počítače může dělat naprosto cokoli, běžná práce jako správce nebezpečná
- Výchozím nastavením Ubuntu je, že účet roota je zamčen, deaktivován.
- Odemčení roota: sudo passwd root
- Uzamčení roota: sudo passwd –l root
- Rootem se stává uživatel, pokud UID = 0, nemusí se však jmenovar ROOT

## Základní příkazy pro práci s uživateli
- `getent passwd [group]` – kteří uživatelé (skupiny) jsou aktuálně zavedení v systému
- `getent group | grep sudo` – vypíše skupinu uživatelů sudo
- `who` – kdo je zrovna přihlášen
- `id pepa` – zjistí v jakých skupinách je pepa
- `find / -user pepa` – hledá vše vytvořené uživ. Pepa
- `Vigr` – zjistíme další skupiny

## Změna hesla
- `Passwd jakub` – nastavím heslo uživateli jakub
- `Passwd` – měním heslo sám sobě

## Profil uživatele
- slouží k individualizaci systému pro uživatele
- `etc/skel` – výchozí profil uživatele = obsahuje soubory, které jsou zkopírovány do domovského adresáře nově vytvořeného uživatele příkazem useradd
- `/home/Jmeno uživatele` – správně nastavený domovský adresář uživatele, musíme zadat parametr `-m`
- Zajišťuje administratorovi, že všichni uživatelé budou mít stejné výchozí nastavení - `/etc/default/useradd`

## Přidání, odebrání editace uživatelů a uživatelských skupin
- Interaktivně
    - Má průvodce, umožňuje zadat parametry
    - `adduser [nazev]` - přidá uživatele
    - `addgroup [nazev]` - vytvoří skupinu
    - `adduser  [nazev] [nazev_skupiny]` - přidá uživatele do skupiny
    - `deluser [nazev]` – smaže uživatele
    - `delgroup [nazev]` – smaže skupinu
    - `Moduser [nazev]` – změna uživatele
- Neinteraktivně 
    - Používá pouze parametry, musím znát přesnou syntaxi
    - `useradd -m [nazev]` -přidá uživatele a vytvoří mu domovský adresář, musíme mu nastavit heslo
    - `userdel` – smaže uživatele
    - `groupadd` – přidá skupinu
    - `groupdel` – smaže skupinu
    - `usermod –a -g [nazev skupiny] [jmeno]` změna uživatele přidá jej do další skupiny

## Nahrazení identity
- `su [jmeno]` – skočí na jiného uživatele (su prachard), přemění nás na jiného usera, musíme znát heslo daného usera, pokud nejsme root, mám práva jako daný uživatel
- `su` – nás přepne na roota
- Když chceme zpět na nás musíme zapsat exit
- `su –c [cat /etc/shadow] root` – povolí příkaz na 1 použití
- Musí se zadat heslo uživatele, kterého chci použít

### Delegování práv
- `sudo` = dočasný správce
- Potřebuji mít práva jako root, ale z důvodu bezpečnosti, nesdělím heslo k rootu k tomu slouží sudo, přidělím člověku oprávnění, pro vykonávání příkazů pro určité uživatele a skupiny, které mu zařídím.
- `visudo` – práce se sudo (otevírá soubor `/etc/sudoers`, kontroluje syntax)
#### Použití:
- Pokud mám v sudo povoleno využívat práva pouze jednoho uživatele:
    - `sudo` příkaz
- Pokud mám v sudo povoleno využívat práva více uživatelů:
    - `sudo uživatel` příkaz
- Poté zadám SVÉ heslo
    - Pokud je v konfiguráku parametr `NOPASSWD`: tak se mne na heslo neptá
#### Uživatelé
-  User privilege specification
- `spravce ALL=(ALL) ALL`
- `pepa localhost=(jirka) /bin/kill`
- `admin ALL= NOPASSWD: ALL !/bin/kill`
- Struktura: `uživatel na_jakych_hostech=(práva_jakých_uživatelů) jaké_cesty !jake_cesty_vynechat`
- Správce může na všech hostech používat všechny příkazy/cesty s právy všech uživatelů
- Pepa může na tomto počítači používat příkaz kill s právy jirky = může ukončovat jeho procesy
- Admin může na všech hostech používat všechny příkazy kromě příkazu kill s právy ROOTA
#### Skupiny
- Pro skupiny platí stejná pravidla jako pro uživatele a zapisují se do stejné sekce, pouze se před ně píše znak %
- User privilege specification
- `%spravci ALL=(ALL) ALL`

### Aliasy
- Pokud se některé volby používají opakovaně, můžeme jim přidat alias
- Host alias specification
- `Host_Alias KANCELAR = 192.168.0.0/24`
- User alias specification
    - `User_Alias SPRAVCI = spravce,jarda`
    - `User_Alias UZIVATELE = pepa,jirka,lenka,franta`
    - `User_Alias VSICHNI = %zaci,%ucitele`
- Runas alias specification
    - `Runas_Alias OP` = operator
- Cmnd alias specification
    - `cmnd_Alias HALT = /sbin/halt`
    - Rozdíl mezi **User_Alias** a **Runas_Alias** je ten, že pokud něco definujeme v Runas_Alias, tak to můžeme použít v () – tedy že chceme, aby uživatel měl práva těchto uživatelů
### Pseudouživatelé
- systémoví uživatelé
- jednotlivé služby/systém si vytvářejí pro své procesy uživatele - aby jim přidali práva k určitým souborům

