# Práce s disky

## Souborové systémy

- způsob organizace a ukládání dat na paměťovém médiu
- zprostředkovává funkce adresářů, souborů a oprávnění

**Vlastnosti souborových systémů:**

- maximální velikost paměťového média (disku)
- maximální velikost souboru
- maximální délka jména souboru
- počet do sebe vnořených adresářů
- podporované znakové sady
- journaling

**Příklady souborových systémů:**

- EXT4 - linux default
- FAT32/FAT64 - jednoduchý souborový systém, používán na Windows před NTFS, kompatibilní se všemi platformami, používán pro USB přenosné disky
- NTFS - Windows
- Btrfs - rychlejší na SSD, systém záloh - snapshots

## Systémové soubory

- `cat /proc/partitions` - seznam disků
- `df -h` – informace o discích
- `cat /etc/fstab` – jaké oddíly se budou automaticky připojovat

## Bloková zařízení

- `blkid` – jak jsou momentálně naformátované zařízení a jejich UUID (ID blokových zařízení), informace o diskových oddílech
- Natrvalo se disky připojují přes UUID, po restartu systému se sám znova napojí

## Vytváření oddílů na discích

- `fdisk /dev/sda` - interaktivní režim
- `fdisk -l` - výpis aktuálního stavu
- `fdisk -l /dev/sda` - široký výpis konkrétního zařízení

```
  DOS (MBR)
   a   toggle a bootable flag
   b   edit nested BSD disklabel
   c   toggle the dos compatibility flag

  Generic
   d   delete a partition
   F   list free unpartitioned space
   l   list known partition types
   n   add a new partition
   p   print the partition table
   t   change a partition type
   v   verify the partition table
   i   print information about a partition

  Misc
   m   print this menu
   u   change display/entry units
   x   extra functionality (experts only)

  Script
   I   load disk layout from sfdisk script file
   O   dump disk layout to sfdisk script file

  Save & Exit
   w   write table to disk and exit
   q   quit without saving changes

  Create a new label
   g   create a new empty GPT partition table
   G   create a new empty SGI (IRIX) partition table
   o   create a new empty DOS partition table
   s   create a new empty Sun partition table
```

## Vytváření souborových systémů

- `mkfs` – formátování oddílů disku
- `mkfs.ext4 /dev/sdb1` – vytvoří systém ext4 na sdb1

## Připojování disků

- `mount` – ukáže připojené disky
- `(u)mount /dev/sdb1 /media/sdb1` = (od)připojím disk sdb1 do složky /media/sdb1
- Do restartartu

## Trvalé připojení

- `vi /etc/fstab` = pokud chci disk připojit natrvalo, musím ho zapsat sem
- reboot

## Přípojné body dle základních druhů instalace

- `/media`
- `/mnt`
- Můžeme však připojit kdekoliv jinam

## Kontrola, oprava a lazení souborového systému EXT

- `tune2fs` – slouží k ladění souborového systému
- `fsck` – kontrola ext4
- `fsck` /dev/sdb5
- `dumpe2fs` /dev/sdb6 - Podrobnější výpis

## Monitoring stavu disků

- `df` – stav disku
- `df –i` – ukáže počet inoudů (počet souborů a složek)
- `du` – spočítá velikost souborů nebo složky
- `mount` – ukáže připojené disky
- `fdisk –l /dev/sda` – jak je rozdělen disk
- Nástroje smartmontools

## Diskové quoty

- `apt-get install quota quotatool`
- `vi /etc/fstab` – přidáme k disku usrquota nebo grquota
- `quotacheck -ugmf /media/sdb1` - zkontroluj quoty
- `quota` - ukáže jaké má přihlášený uživatel quoty
- `setqouta jura 15000 20000 8 10 /media/sdb1/` - limity quoty pro sdb1, pro uživatele jura
  - soft limit (8) - je to limit, tedy počet souborů a složek, které si může uživatel uložit. Po 7 dnech po překročení se ze soft limitu stane hard limit
  - hard limit (10) - maximální počet souborů a složek, které může uživatel uložit.
- `df -i` - vypíše obsazenost disků z pohledu inoude (uzly)
- `quota -u jura` - řekni mi co víš o uživateli jura (jaké má kvóty)

## Kopie svazků

- pro kopírování celých oddílů disků nebo celého disku a můžu vytvořit obraz disku,
- kopíruje po blocích
- Hlavní parametry jsou if a of, přičemž pomocí if se zadává vstupní soubor (input file) a pomocí of tedy výstupní soubor (output file).
- `dd if = dev/sda1 of=dev/dev/sdb`

## SWAP

- když je plná paměť ram, systém si zde odkládá data.
- `swapon`, `swapoff` – zapne, vypne swap
- `swapon /dev/sdb5` – aktivuje swap na sdb5
- `swapoff –a` – vypně všechny swapy
- Mkswap /dev/sdb6 – vytvoří swapovací oddíl na sdb6

## S.M.A.R.T.

- **Tři funkce:**
  - shromažďuje řadu údajů o možném budoucím selhání
  - pokud zjistí nějakou chybu při práci s diskem, pak ji zaznamená do svého vnitřního logu
  - testování disků na povel, tedy jakási vnitřní samodiagnostika
- pro práci s ním se používá smartmontools
- `cat /etc/Smartd.conf` – monituruje stav disku a informuje o něm
