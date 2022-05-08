# Bezpečnost dat a služba SSH

## Systémové soubory

- `/etc/passwd`
  - Zobrazí info o uživatelích v následujícím tvaru: `username:password:userID(UID):maingroup(definováno pomocí GID):GECOS(user info):user_home:user_shell`
  - je pro všechny ke čtení (`cat /etc/passwd` – zobrazí práva)
  - Když je u hesla `*` - heslo je zablokované
  - Když je u hesla `X` – heslo je stínové, hledá se v souboru `/etc/shadow`
  - `md5sum` – hashující algoritmus (`md5sum blebleble` – zahashuje blebleble)
  - UID == 0 ► root
  - 0 < UID > 1000 ► systém. uživatelé (služby)
- `/etc/shadow`
  - smí číst pouze root a skupina root (`cat /etc/shadow` – zobrazí práva)
  - obsahuje stínová hesla, odkazuje sem soubor `/etc/passwd`
  - `user:password:parametry`
  - Heslo je zahashované
  - **Parametry:**
    - Poslední změna hesla: Days since Jan 1, 1970 that password was last changed
    - Minimum dnů, které musí uplynout pro možnost další změny hesla
    - Maximum dnů, po které je heslo platné, než se bude muset změnit
    - Počet dnů před tím než bude uživatel varován, že mu končí heslo
    - Počet dnů kdy je účet po vypršení hesla nedostupný
- `/etc/sudoers`
  - obsahuje záznamy, kdo může použít sudo s právy kterého uživatele
  - Struktura viz. 21.Systémoví uživatelé a skupiny
  - Smí zapisovat pouze root (`cat /etc/sudoers` – zobrazí práva)
- `/etc/nsswitch.conf`
  - zabezpečit souborovým oprávněním
  - kde se mají hledat základní informace (uživatelé, skupiny, hesla, hosti, sítě,...)

## Souborová oprávnění

- 4 části po 3 bitech čili 12Bitů
- 1-3 bit ► speciální oprávnění (2 na 3 = 8 druhů oprávnění) - **oktální**
- 4-6 bit ► user (první 3)
- 7-9 bit ► group (druhé 3)
- 10-12 ► others (třetí 3)
- Práva:
  - `0` ► Nic
  - `1` ► Executable
  - `2` ► Write
  - `3` ► X Write
  - `4` ► Read
  - `5` ► RX
  - `6` ► RW
  - `7` ► RWX
- `ls -l` - vypíše souborová oprávnění
- `chmod 740 pokus1` (skupina User může vše, Group je R – jenom číst a skupina Others nemůže nic - 0)
- `chmod u(g,o)-s(x,w,r) pracovni/` - odebere userovi právo s na složce pracovni
- `chmod u=rwx pracovni/` - přidá userovi r,w,x na složce pracovni

- **Změnu vlastnictví** může provádět pouze root
  - `chown karel pokus` – změní vlastníka ve složce pokus na karla
  - `chgrp ucitele pokus` – změní skupinu ve složce pokus na ucitele

## Disková pole RAID

### Základní typy RAID a jejich vlastnosti

#### RAID 0

- Stripping (Prokládání) – půlka dat se ukládá na 1 disk, druhá půlka na 2
- Při poruše jednoho z disků jsou soubory porušeny
- Rychlejší zápis a čtení

#### RAID 1

- Mirroring (Zrcadlení) – Cokoliv se provede na 1 disku, se provede i na 2.
- V případě výpadku jedno disku (porucha) se automaticky přejde na disk 2. a všechna data jsou zachována
- Potřeba dvojnásobná kapacita

#### RAID 5

- Vyžaduje alespoň 3 disky
- Data jsou rozdělena mezi disky, spolu s nimi samoopravné kódy
- Rychlejší čtení, pokud jeden disk vypadne – samoopravné kódy zajistí neporušení záznamů po přidání nového disku

### Vytvoření, monitoring a správa - nástroj MDADM

- `mdadm` – vytváření raidu
- `ls /etc/init.d/mdadm` – vypíše jaké raidy jsou momentálně v provozu (startovací script)
- `mdadm --create /dev/md1 --level=1 --raid-devices=2 /dev/sdc1 /dev/sdc2 ---spare-devices=1 /dev/sde1` - vytvoření raidu
- `cat /proc/mdstat` – ukáže vytvořené RAIDY
- `mdadm –D /dev/md1` – nejpodrobnější výpis
- `cat /etc/Smartd.conf` – monituruje stav disku a informuje o něm

## Záloha dat

- komplexnost - měl bych mít zálohováné všechno
- aktuálnost - zálohovaná by měla být poslední verze
- více možných stavů - ne jenom poslední stav a i starší
- pravidelnost - plán záloh
- automatizace
- bezpečnost
- neduplicita záloh

### Druhy záloh:

- Zálohování - `rdiff-backup soubor`
- Opakovatelná nastavení v `cron`

#### prostá kopie

- nesplňuje požadavek na neduplicitu dat, zkopíruje vše

#### rozdílová záloha

- vytvoří nultou kopii jako prostou a další zálohy se zálohují jako rozdíl vůči nulté záloze

#### přírůstková záloha

- zálohuje pouze změny, vždy rozdíl vůči předchozímu stavu (obnova trvá výrazně déle)

### archivační a zálohovací nástroje

- archivace – více souborů do jednoho
- komprimace – zmenšení velikosti souboru

#### Tar

- vezme složky, soubory a zabalí je do jednoho
- `tar cvf etc.tar /etc` – vytvoří zálohu etc do souboru etc.tar

#### Gzip

- `gzip *.txt` – komprimování
- `gzip -d *.zip` - dekomprese

### Synchronizace dat

- `rsync` (synchronizace dat)
- dokáže synchronizovat soubory a složky z jednoho umístění do jiného.
- minimalizuje objem přenášených dat

```bash
rsync -av /home/uzivatel/dokumenty /mnt/zaloha/
```

## SSH

- SSH umožňuje bezpečnou komunikaci mezi dvěma počítači, která se využívá k jakémukoliv obecnému přenosu dat
- na cílový počítač instaluju SSH Server
- na počítač ze kterého se hlásím, instaluju SSH Klienta
- Instalace serveru: `apt-get install openssh-server`
- Instalace klienta: `apt-get install openssh-client`
- Server může být i klientem

### Základní použití SSH klienta

- přihlášení klienta

```bash
ssh user@server
```

- zkopíruje veřejný klíč klienta na server, aby ses mohl připojit k serveru
- automaticky ho přejmenuje na požadované jméno (aspoň mě to tak udělalo)
- `ssh-copy-id –i /honza/.ssh/id_dsa.pub michal@192.168.1.1`
- po provedení se můžu přihlásit přes ssh

```
ssh-copy-id –i /cesta/ke/klici user@host
```

- agent ssh drží klíč v paměti a použije ho podle potřeby

```
ssh-add ~/.ssh/id_rsa
```

#### scp

- protokol scp slouží k přenosu souborů mezi 2 disky
- `-i autorizacni_klic`
- kopírování mezi dvěmi pc
- `scp -i /~/.ssh/id_rsa ~/.ssh ~/soubor user@host:~/kopie`

```
scp soubor kopie
```

### Druhy klíčů

- Ke komunikaci je třeba mít 2 páry klíčů:
- První, vytvořen automaticky = klíč pro komunikaci
- druhý, který musíme vytvořit ručně = klíč pro autentizaci
- Jeden pár tvoří Veřejný a Privátní klíč
- Soubor se zašifruje pomocí Veřejného klíče a lže být dešifrován pouze pomocí odpovídajícího Privátního klíče = Asymetrické šifrování

### Šifrování

- SSH používá Asymetrické šifrování:
- Používá dva klíče – Veřejný a Privátní, na rozdíl od Symetrického šiforvání, které pro zašifrování a rozšifrování používá stejný klíč

### Certifikáty

- Vygenerován, není potřeba hromada klíčů, pro použití autentizaci se na daný stroj ukládá jen předmět certifikátu (hlavička -jméno apod.)

### Soubory klíčů

- Veřejné klíče (hostkeys) mají příponu PUB, privátní ne
- Klíče jsou pouze texťáky
- Veřejné klíče klientů se musí uložit do slozky, která je zapsána v sshd_config #AuthorizedKeysFile
- `ssh-keygen -t dsa` (vygeneruje pár klíčů dsa)
- Veřejný klíč na serveru se musí jmenovat podle konfigurace SSHD (výchozí Authorized_Key)
- Soukromý klíč na klientovi se jmenuje buď id_dsa/id_rsa nebo se jmenuje idenitit, nebo jakkoliv
- Soukromý klíč pro autorizaci by měl být vždy zabezpečen heslem
- i když někdo ukradne certifikát, musí ještě znát heslo

### Fingerprint

- Část klíče, kterou můžeme zkontrolovat, abychom si byli jistí, že je to klíč toho klienta, kterého chceme
- `ssh-keygen /cesta/ke/klici `- zjistím firgerprint

### Konfigurace a zabezpečení SSH serveru

- `/etc/init.d/ssh` – služba (`systemctl status sshd`)
- `/etc/ssh/` - configuráky
- `/etc/ssh/ssh_config` – konfigurace na stanici
- `/etc/ssh/sshd_config` – konfigurace serveru

```bash
 # /etc/ssh/sshd_config
AuthorizedKeysFile /cesta/souboru # kam se ukládá veřejný klíč
 # pro autorizace klienta na serveru
PermitRootLogin no # pro bezpečnost ► útočník se nedostane přes SSH na roota
AllowUsers user1 user2 # kteří useři se smí připojit na SSH server
```

**způsoby autorizace:**

- Heslo (Výchozí)
- Kerberos
- Pomocí klíčů, certifikátů

### Základní použití bezpečného přenosu dat prostřednictvím ssh.

- SSH poskytuje zabezpečený vzdálený přístup k serveru
- Pomocí protokolu SCP můžeme také kopírovat soubory ze serveru na klient
- Může také sloužit jako šifrovací tunel pro ostatní aplikace
