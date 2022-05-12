# Síťové služby pro sdílení dat NFS, Samba, Apache

## Apache

- Nejrozšířenější webový server
- Instalace serveru, démon a startovací skript
- `apt-get install apache2`
- Startovací script - `/etc/init.d/apache2`
- Démon `apache2`

### Struktura konfiguračních souborů, správa modulů

- `/etc/apache2/` - obsahuje konfiguráky
- `/etc/apache2/apache2.conf` – hlavní konfigurák, je v něm zobrazena struktura celé konfigurace

```
etc/apache/
├── apache2.conf/
│   └── ports.conf
├── mods-enabled/
│   ├── *.load
│   └── *.conf
├── conf.d/
│   └── *
└── sites-enabled/
    └── *
```

- `/etc/apache2/mods-available` - dostupné moduly
  - Pokud zde nenajdeme modul, který hledáme, doinstalujeme ho pomocí `apt-get`
- `/etc/apache2/mods-enabled` - zavedené moduly (pouze symbolické linky do available)
  - Můžeme vytvořit ručne nebo pomocí předchystaného scriptu a2enmod
- `/etc/apache2/sites-available` - dostupné stránky
- `/etc/apache2/sites-enabled` - zavedené stránky (pouze symbolické linky do available)
  - Můžeme vytvořit ručne nebo pomocí předchystaného scriptu a2ensite
- `/etc/apache2/envars` - základní systémové proměnné pro apache
- `.htaccess` - lokální konfigurace apache pro daný adresář - není třeba roloadnout server - pokud chceme používat, musí se povolit

#### Moduly php5 a userdir

- Modul `php5` umožňuje používání php na serveru
- Userdir povoluje uživatelům sdílet obsah jejich home adresářů
  - `a2enmod userdir`
  - `/etc/apatche/apatche2.conf`
    - Přidám řádek `UserDir public_html`
    - = povolil jsem userdir v adresáři `public_html`
  - Uživatel vytvoří adresář přesně podle zadaného jména ve svém homu, práva musí být `rx`
  - K webu přistupujeme `www.webovastranka.cz/~uzivatel`

### Konfigurace virtuálních webových serverů

- Vytvoříme DNS záznam který chceme, aby nás odkazoval na daný virtuální web
- Vytvoříme složku, do které vložíme virtuální web
  - Nejlepší postup:
    - Defaultní web přesuneme ze složky `/var/www` do složky `/var/www/default`
- Vytvoříme složku pro nový web - `/var/www/novyweb` (můžeme ji však vytvořit kdekoliv jinde)
- V `/etc/apache2/sites-available/` vytvoříme soubor pro náš web – zkopírujeme default a upravíme nebo můžeme taky používat default
  - Pro každý virtual web musíme vytvořit sekci `<VirtualHost _:80></VirtualHost _:80>`
  - Do této sekce zapíšeme `ServerName doménu.virtualniho.webu`
  - A poté ještě `DocumentRoot /cesta/k/webu`
  - Můžeme přidat další direktivy

```bash
<VirtualHost *:80>
  ServerName nsl.doma
  ServerAdmin webmaster@localhost

  DocumentRoot /var/www
  <Directory />
    Options FollowSymLinks
    AllowOverride None
  </Directory>
  <Directory /var/www/>
    Options Indexes FollowSymLinks MultiViews
    AllowOverride None
    Order allow,deny
    allow from all
  </Directory>

  ScriptAlias /cgi-bin/ /usr/lib/cgi-bin/
  <Directory '/usr/lib/cgi-bin'>
    AllowOverride None
    Options +ExecCGI -MultiViews +SymLinksIfOwnerMatch
    Order allow,deny
    Allow from all
  </Directory>

  Errorlog ${APACHE_LOG_DIR}/error.log

  # Possible values include: debug, info, notice, warn, error, crit,
  # alert, emerg.
  LogLevel warn

  CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
<VirtualHost *:80>
  ServerName www.doma
  DocumentRoot /var/novyweb
</VirtualHost>
```

- V reálné situaci nám DNS spravuje někdo jiný => nevytváříme záznam DNS, pouze ho použijeme

### Zabezpečení složky uživatelským jménem a heslem

- Ve složce `vim .htacces`
  - `require valid-user` = přístup pouze pro ověřené usery
  - `htpasswd –c .htpasswd zbynda` = vytvoření usera

## Samba

- Umožňuje sdílet složky a tiskárny na linuxovém serveru a připojovat je z windowskovského klienta, jako datový zdroj může využívat Files (lokální soubory), nebo například **LDAP** (něco jako Active Directory)
- Může vystupovat jako **Primary domain controller**

### Instalace serveru, démoni a startovací skript

- `apt-get install samba`
- `/etc/init.d/samba` – startovací skript
- `smbd` – démon, který se stará o sdílení souborů a složek
- `nmbd` – démon, který řeší pojmenování stanic v protokolu netBIOS
- `smbstatus` – v jakém stavu se nachází samba

### Základy konfigurace, vysvětlení základních sekcí

- `/var/lib/samba` – soubory samby
- `/etc/samba/smb.conf` – základní konfigurák
- Sekce `global`
  - Globální nastavení (workgroup, do jaké sítě je sdílená, logování, šifrování hesla)
- Sekce `homes`
  - Nastavení sdílení domovských adresářů (s jakými právy jsou sdíleny, komu)
- Sekce `netlogon` (nejde vidět, pokud používáme testparm)
  - Logovací skripty
- Sekce `profiles`
  - Cestovní profily (má smysl, pokud používám Sambu jako doménový řadič (Active directory))
- Sekce `printers`
  - Nastavení sdílení tiskáren

### Správa účtů uživatelů, skupin a stanic

- Uživatelé v sambě musí být první zavedeni i v systému
- `smbpasswd `– základní práce s uživateli (vytvoření/odebrání,..)
  - `smbpasswd –a zbynda` – přidá uživatele zbynda
- `pdbedit` – pokročilá práce s uživateli (nastavení domácích adresářů, dísků, logon skripty, profily, account policy)
  - `pdbedit –l` – vypíše veškeré uživatele
- `SSID` = ID Domény
- `SSID` + `UID` = User SID
- `SSID` + `GID` = Group SID

### Základní nástroje pro diagnostiku

- `testparm` - zkontroluje správnost konfiguráku, vypíše čístý konfigurák bez komentářů

### smbclient, připojení svazku cifs

- **smbclient**
  - `apt-get install smbclient`
  - `smbclient --list=router --user=zbynda` (podívám se, co mi nabízí zbynda na routeru)
  - `smbclient \\\\router\\zbynda --user=zbynda` (můžu s tím pracovat) – ukončím `quit`
- **cifs**
  - `apt-get install cifs-utils`
  - `mkdir /media/router-cifs-zbynda`
  - `mount –t cifs –o username=zbynda, password kokos, rw //router/zbynda /media/router-cifs-zbynda`

## NFS – Network file system - Sdílení

- Sdílení dat mezi linuxovými počítači
- Výhody:
  - Jednoduchost nastavení
  - Rychlost přenosu dat
- Nevýhody:
  - Zabezpečení

### Server

- Nainstaluju `nfs-kernel-server`
- Poskytuje diskový prostor

### Klient

- Nainstaluju `nfs-common`
- Využívá nasdílený diskový prostor ze serveru
