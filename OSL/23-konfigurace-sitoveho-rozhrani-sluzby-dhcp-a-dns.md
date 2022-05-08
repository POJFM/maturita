# Konfigurace síťového rozhraní a služby DHCP a DNS

## Konfigurace sítového rozhraní

### Systémové soubory

- `/etc/network/interfaces`

```bash
auto eth0  #startuje s démonem (runlevely)
allow-hotplug eth0 #zapne po připojení kabelu, vypne po odpojení
iface eth0 inet static
    address 192.168.1.2
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-server 192.168.1.1

post-up echo “nameserver 192.168.1.1” >> /etc/resolv.conf # potom co nastartuješ síťovku proveď
 # pre-up před nastartovaním síťovky, pre/post-down před/po vypnutím síťovky
```

- `/etc/hosts`
  - Lokální záznamy dns
  - Jedno IP může mít více názvů
- `/etc/resolv.conf`
  - Knihovny resloveru se starají o to, kdo bude překládat (hledá dns servery)
- `/etc/nsswitch.conf`
  - Kde se mají hledat základní informace (uživatelé, skupiny, hosti, sítě, ...)
- `/etc/networks`
  - Pojmenování sítí
  - `name net-ip`

### Základní příkazy pro konfiguraci rozhrání, diagnostika

- Základní rozhraní:
  - `lo` - loobback
  - `eth0` - ethernet
  - `wlan` – WiFi
  - `TUNTAB` - VPN - virtuální privátní síť
  - `PPP` - podpora starých modemů
- `/etc/network/` - základní konfigurace
- grafické desktopy používají démona `networkmanager`
- `hostname` – změna jména počítače (`vim /etc/hostname` - jinak to po restartu nezůstane)
- `ifconfig` – vypíše pouze aktivní síťová rozhraní (pro všechny rozhraní parametr –a)
- Základní příkaz pro nastavení sítě
- `ifconfig eth0 192.168.1.2 netmask 255.255.255.0 up` - nastaví síť (po restartu démonu se nastavení smaže ► pro trvalé nastavení musíme zapsat do `/etc/network/interfaces`)
- `ifup`/`ifdown` – nastartuju nebo vypnu konkrétní síťové rozhraní (`ifup eth0`)

### Démon networking

- `/etc/init.d/networking`
- `systemctl status networking`

### Základy statického směřování IPv4

- `route` ► vypíše routovací tabulku
  - `paramter –n` ► vypíše v číslech
- `route add -net 192.168.2.0/24 gateway 192.168.1.5`
  - přidání záznamu do routovací tabulky ► pokud chceš jít do sítě `192.168.2.0/24 `běž přez bránu `192.168.1.5`
  - místo -net ip_sítě/prefix může být -host ip_hosta => chceš li jít k hostovi ip_hosta běž přez bránu 192.168.1.5
- `cat /proc/sys/net/ipv4/ip_forward`
  - vypíše `0` nebo `1`
  - `0` ► zakázáno směrování
  - `1` ► povoleno směrování
  - změním to ► `echo 1 > cat /proc/sys/net/ipv4/ip_forward`

### Lokální předklad doménových jmen a základní konfigurace resolveru.

- `/etc/hosts`
  - Lokální záznamy dns
  - Jedno IP může mít více názvů
  - Používá se pro menší domény (3-5 PC)
- `/etc/resolv.conf`
  - Knihovny resolveru se starají o to, kdo bude překládat (hledá dns servery)
  - `domain` - v případě že počítač je zařazen do jedné dns domény a ta se používá primárně pro vyhledávání ► `ping pc02` (automaticky k tomu přidá tuto doménu)
  - `search` - při hledání ve více doménách, oddělují se mezerou

## Sítové služby DHCP a DNS

### DNS - Domain Name Server

- Systém doménových jmen
- kořenová doména se značí tečkou
- TLD (Top Level Domain) - domény 1. řádu (.cz, .eu, .net)
- domény 2. řádu (seznam, google)
- 3 řád www., mail., ftp.
- FQDN = full qualified domain name = plně kvalifikovaný doménový název (www.linuxexpres.cz)
  - `mail.spsoafm.cz`
  - `ftp.spsoafm.cz`
  - `print-v1.zaci.spsoafm.cz`
  - `PC01E106.zaci.spsoafm.cz`
  - `notebook-pospech.ucitele.spsoafm.cz`

### Konfigurace resolveru

- Knihovny resloveru se starají o to, kdo bude překládat (hledá dns servery)
- `domain` - v případě že počítač je zařazen do jedné dns domény a ta se používá primárně pro vyhledávání = ping pc02 (automaticky k tomu přidá tuto doménu)
- `search` - při hledání ve více doménách, oddělují se mezerou

### Druhy DNS serveru a DNS dotazy

- **Dotaz na DNS**
  - `host www.seznam.cz`
  - `host www.seznam.cz localhost` (můžeme zadat koho se ptáme – ptáme se localhostu)
  - `nslookup www.seznam.cz`
  - `dig www.seznam.cz` (nejpodrobnější)
- **Druhy DNS serverů**
  - Autoritativní
    - Spravuje vlastní zónové záznamy pro danou doménu, obvykle jsou alespoň 2 dva takovéto servery – primární a záložní (tzv. „slave“)
  - Cacheovací
    - Dočasně ukládá DNS dotazy
  - DNS server může běžet současně ve více rolích, prakticky vždy běží jako cacheovací, pro nějakou doménu může být autor. primární, pro jinou může být autor. záložní. Záložní by se měl synchronizovat s primárním po určité době.

### Instalace démona

- `apt-get install bind9`
- `/etc/init.d/bind9` – démon

### Konfigurace DNS serveru BIND

- `/etc/bind/` - konfiguráky
- `/etc/bind/db.vyuka`

### registrace zón,

- `/etc/bind/named.conf.local` - registrujeme vytvořené zóny
- `/etc/bind/named.conf.default-zones` - obsahuje defaultní zónové soubory (localhost, broadcast)
