# Active Directory

- Rozšiřitelná adresářová služba umožňující spravovat prostředky na doménovém řadiči (slouží pro něj něco jako základ)
- Poskytuje celkový přehled o objektech v síti (např. účty, počítače, tiskárny)
- Umožňuje využívat stromovou strukturu objektu, nastavovat globální politiky, spravovat software na počítačích
- Jedná se o distribuovanou databázi tzn. části databáze jsou přenášeny do jednotlivých PC v doméně, obsahuje informace o nastavení PC a uživatelů v doméně
- Je nástrojem centrální správy

### Funkce

- Je založena na standardních internetových protokolech
- Jednoznačně definuje strukturu sítě
- Organizuje skupiny počítačů a domén

- Vyžaduje instalaci služby DNS
- Nutno povýšit na DC (doménový řadič)
- Instalace služby Active Directory: Start🡪Spustit🡪otevřít: dcpromo (OK)
    - Ve win12 je automaticky 🡪 stačí proto jen povýšit na DC přes role

### Služba AD obsahuje logické i fyzické struktury sítě

**Logické**

- **Organizační jednotky** - podskupiny domén, které často odpovídají obchodní nebo řídící struktuře organizace
- **Domény** - skupiny počítačů sdílejících společnou adresářovou databázi
- **Stromy domén** -  jedna nebo více domén sdílejících souvislý obor názvů
- **"lesy" domén** -  jeden nebo více stromů domén sdílejících společné adresářové informace

**Fyzické**

- **Podsítě** - síťová skupina se specifickým rozsahem IP adres a masky podsítě
- **Sítě** - jedna nebo více podsítí, slouží ke konfiguraci přístupu k adresářové službě a replikací

- Logické struktury pomáhají při organizaci objektů adresářové služby a při správě účtů a sdílených prostředků sítě
- Fyzické struktury usnadňují komunikaci v síti a fyzicky ohraničují prostředky sítě

## Doména active directory
Skupina počítačů, které sdílejí společnou adresářovou databázi
Základní jednotka je AD, tvoří ji minimální 1 doménový řadič
Je bezpečnostní hranice ve struktuře Active direktory
Má jednoznačné zařízení
Má vlastní zásady a zabezpečení
Vytváří vztahy důvěry s ostatními doménami
