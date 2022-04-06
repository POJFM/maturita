# Základy operačního systému GNU/LINUX
- Open-source software a projekt GNU
- Distribuce GNU/Linux
- Souborový systém
    - Organizace souborového stromu
    - Základní příkazy pro práci se soubory, adresáři, linky, hledání souborů, typy souborů
- Spouštění a vypínání systému
    - daemoni a startovní skripty
    - úrovně běhu
- Procesy
    - Vlastnosti procesu
    - Sledování, řízení procesů
- Plánování úloh
    - jednorázové úlohy
    - opakované úlohy
- Monitoring systému
    - Logovací soubory a základní příkazy pro práci
    - Monitorig logů
    - Rotace logů

## Operační sytém
- základní programové vybavení počítače
- je zavedeno do paměti počítače při jeho startu
- zajišťuje uživateli ovládání pc
- přiděluje procesům systémové zdroje
### Složení OP:
- **Kernel** – jádro operačního systému
- **Shell** – rozhraní pro uživatele UI, 
    - může být textové/příkazové CLI ( Comand Line Interface)
    - grafické GUI (Graphic User Interface
## Open-source software a projekt GNU
- **GNU** – projekt svobodného operačního systému, který je zdarma, nezávislý, má přístupný kód
- svoboda používat program za jakýmkoliv účelem
- svoboda studovat, jak program pracuje a možnost přizpůsobit ho svým potřebám
- svoboda redistribuovat kopie programu.
- svoboda vylepšovat program a zveřejňovat zlepšení, aby z nich mohla mít prospěch celá komunita
### Koncepce systému GNU/Linux 
- víceúlohový systém – úlohy běží současně
- víceuživatelský systém – více uživatelů může pracovat současně
- textové a možnost grafického rozhraní
- modulární systém – snadná aktualizace a modifikace systému
- standardizovaný

## Distribuce GNU/Linux
- linuxový systém založený na Linuxovém jádru, který je doplněn o aplikační software tvořící aplikační celek. 
- Obvykle je založen na licenci GNU (open source software).
- Některé distribuce obsahuji komerční aplikační software
- **Příklad Distribucí:** Ubuntu, Debian, Suse, Slackware, Fedora

### Souborový systém
- Adresářová struktura
- Nejvyšší úroveň je kořen /
- Následují pod adresáře a další soubory , stromová struktura

### Základní adresáře
- `/boot` – obsahuje jádro operačního systému a konfiguraci zavaděče operačního systému zavaděče Grub a Lilo
- `/bin` – obsahuje základní příkazy operačního systému
- `/dev` – obsahuje soubory zařízení, každé zařízení je reprezentováno souborem, prostřednictvím kterého lze s daným zařízením pracovat
- `/etc` – obsahuje konfigurační soubory
- `/home` – domovské adresáře uživatelů (ne root), měli by být vždy na samostatném oddíle nebo disku
- `/lib` – obsahuje systémové knihovny
- `/lost+found` – po kontrole disku se zde ukládají nalezené poškozené soubory, je na všech oddílech
- `/media (/mnt)` – místo pro připojení dalších zařízení a oddílů disků. Další zařízení v Linuxu lze připojit kdekoliv v adresářovém stromu, adresář /media popř. /mnt je zažitým standartem.
- `/opt` – obsahuje nestandartní (volitelné) aplikace, které nejsou součástí repozitory systému
- `/proc` – obsahuje virtuální soubory, které si vytváří jádro a dále je udržuje, procesy, 
- `/root` – domovský adresář uživatele root
    - `/sbin` – obsahuje základní příkazy přístupně pro uživatele root
- `/tmp` – pro dočasné soubory, všichni uživatelé zde mají právo zápisu, v případě serveru je vhodné adresář 
- `/usr` - standartní adresář pro umístění aplikačního softwaru (C:ProgramFiles)
- `/var` – proměnné prostředí systému Linux (zálohovat), obsahuje logy (záznamy události OP a aplikací), weby

## Typy souborů
- **F** = běžný, regulární soubor
- **D** = directory (adresář)
- **L** = symbolický link (něco podobného jako Zástupce ve Windows)
- **C** = znakové zařízení (soubor, který pracuje znakově) terminal
- **B** = blokové (čte a zapisuje v blocích; disky, flashky) či znakové (čte a zapisuje sekvenčně) zařízení
- **P** = pojmenovaná roura (používá se v případě předávání procesů) - meziprocesní komunikace
- **S** = socket

## Základní příkazy pro práci se soubory, adresáři
- `cd` – vstoupí do adresáře, cd .. vystoupí o úroveň zpět cd . aktuální adesář
- `pwd` –  aktuální adresář ve kterém se nachází
- `who` – kdo je přihlášen, terminal, datum
- `whoami` – vypíše uživatelské jméno
- `ls` – vylistuje adresář -a výpis všeho, -h výpis přehledně
- `cat` – výpis obsahu souboru
- `mkdir [nazev]` – vytvoření adresáře, mkdir -p svet/afrika/etiopie/ vytvoří vnořené adresáře
- `rmdir [nazev]` – smazání adresáře, ale musí být prázdný
- `rm – rf` – smaže a neptá se 
- `sort` – seřadí podle abecedy
- `touch` – vytvoří prázdný soubor v adresáři
- `nano` / `vi` / `vim` – textový editor, vytvoří soubor txt
- `cp` – kopírování adresáře, cp -r adresáře i s dalšími podadresáři
- `mv` – přesunutí adresáře, přejmenování souboru nebo adresáře
- `Find .` – vyhledá soubory, - name něco* - vyhledá soubor začínající na něco

## Linky
- Rozlišujeme dva typy linků: hardlink a symboliclink
- Link je vlastně odkaz na nějaký soubor
### Symbolický link (SymLink)
- odkaz na soubor, neobsahuje žádná data, 
- při smazání původní soubor zůstává, chová se jako zástupce ve windows
- `ln –s /path/to/file   /path/to/symlink` – vytvoří symbolický link
### Hard link
- Odkaz na soubor, ale obsahuje data souboru
- když se smaže hardlink, smaže se i původní soubor
- `ln – /path/to/file    /path/to/hardlink` - vytvoří se hardlink

## Spouštění a vypínání systému
- Start jádra
- Systém startuje v následujících fázích:
    - **Superblok** = první blok na disku
    - **Jádro** – spouští program init
    - Program init spouští jednotlivé scripty v závislosti na run levelu
    - **Startovací** skripty – inicializují systém, spouštějí démony
    - **Init** – spouští skripty podle konfigurace souboru `/etc/inittab`

## Démoni
- Je to program, který běží na pozadí
- Čeká na události, které nastanou, reaguje na ně a poskytuje služby
- Spouštění skripty jsou v `/etc/init.d`
### Úrovně běhu
- **Runlevel** = sada symbolických linků s pořadovým číslem, které odkazuje na démona (démona buď spouští nebo vypínají)
- Run level je něco jako stav použitelnosti systému 
- Můžeme ho kdykoliv změnit (nejen při startu)
- Máme k dispozici 7 runlevelů:
    - **0** – Halt, ukončení, vypnutí systému
    - **1** – Single user mode, ukončení démonů, deaktivuje se automaticky, je to nouzový režim
    - **2** – Multi user mode, neposkytuje služby jako DNS, NFS, samba atd. (bez síťvého rozhraní)
    - **3** – multi user mode, systém se sítí, spouští se běžným způsbem
    - **4** – nepoužívá se
    - **5** – plnohodnotný stav, stejný jako run level 3 jenom je navíc grafika
    - **6** – restart systému 
- Při spuštění PC se démoni spustí v zadaném run levelu
- Zadáním runlevel zjistíme, v jakém se aktuálně nacházíme

### Systemctl
- Pro práci s démony je možné použít i příkaz systemctl 
- Restartování služby/démona 🡪 systemctl reload demon
- Reload, restart, enable, disable

## Procesy
- Spuštěné programy, algoritmy načtené v operační paměti
- Jeho vlastníkem je uživatel, který jej spustil
- Každý proces má své proces ID (PID), je jedinečné
- Rozdělujeme na procesy
    - Běžící na pozadí
        - Běží přímo v našem terminálu nebo v grafickém terminálu, aplikace
    - Běžící na popředí
        - Říká se jim démoni, nevidíme co dělají, služby

### Sledování, řízení procesů
- `ps` – vypíše procesy, -aux vypíše všechny procesy se všemi informacemi
- `kill` – zabití / ukončení procesu
- `STOP` – zastavení běhu procesů
- `cont` – obnovení procesu
- `PSTREE` – vypíše strom procesů
- `nice` – mění prioritu procesu nejvyšší -20, standartní – 0, nejnižší 19
- `top` – vypisuje procesy, které nejvíce zatěžují systém

## Plánování úloh
- Rozdělujeme na jednorázové a opakované
- **Jobs** = ukáže kolik je spuštěno jobů a jejich stav
### Jednorázové úlohy (AT)
- Abychom mohli použít příkaz at musíme nám běžet démon Atd, který vše řídí 
- Spuštění `Atd /etc/init.d/atd start`
    - Interaktivně:
        - `At 8:45 15.01.2015`
        - Poté píšeme pomocí echo “” (ukončí se Ctrl + D)
    - **Atrm 4** – smaže job 4
    - `ls /var/spool/cron/atjobs` = ukládání naplánovaných jobu

### Opakované úlohy (CRON)
- Systémový démon, který v definovaném čase a datu spustí nějaký proces
    - Plánovač opakovaných úloh
- `crontab –l` = výpis naplánovaných jobu   
- `crontab –e` = konfigurace
    - `10 * * * 4 date >> cron.log` = minuty, hodiny, den v měsíci, každý měsíc, 4 den v týdnu
    - `ls /var/spool/cron/crontabs` = ukládání naplánovaných jobu 
    - `/etc/cron.daily atd.` = systémové joby, pro udržbu systému

## Monitoring systému
- Všechny logy se standartně ukládají do složky /var/log/ (systémové záznamy)
- Logy uchovávají informace o činnosti jednotlivých procesů, aplikací atd.
### Logovací soubory a základní příkazy pro práci
- Rsyslog –  Démon, který má na starost zaznamenávání systémových hlášení (v Debianu rsyslog)
- `/rsyslog.conf` – konfigurák syslogu
- **0** - nejnižší priority logování (emergency)
- **7** - nejvyšší priorita logování (debug)
- zdroj(co).0 až 7 - cíl(kam se log šoupne; např. /dev/xconsole)

#### Logovací soubory:
- `cat /var/log/apt/history.log`
- `cat /var/log/auth.log`
- `cat /var/log/kern.log`
- `cat /var/log/syslog`

### Monitorig logů
- **logcheck** -  posílá konkrétní řádky z logů (využívá joby)
- **logwatch** – zasíla pouze souhrn událostí, popřípadě statistiky
- **swatch** - aktivní monitorovací nástroj pro logy, tzn. umí na hlášky vámi definovaného typu reagovat vámi nastaveným způsobem
- **last** - kdo co a kde naposledy dělal
- `cat /var/log/syslog | head -n 5` - vytáhne prvních 5 řádků
- `cat /var/log/syslog | tail -n 5` – posledních

### Rotace logů
- **Rotace logů** - staré logovací záznamy se zkomprimují a začíná se logovat do prázdných souborů, drží se několik verzí starých logů.
- Program se jmenuje logrotate spouští se cronem(Jobem).
- `cat /etc/logrotate.conf`


