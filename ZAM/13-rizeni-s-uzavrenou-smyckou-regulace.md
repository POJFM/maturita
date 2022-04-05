# Řízení s uzavřenou smyškou - regulace

- **regulace** - umožňuje udržování určitých fyzikálních veličin na stanovených hodnotách, řízení na zpětnou vazbu

## Druhy řízení, druhy regulace

### Vlastnosti členů regulačního obvodu

- statické
  - statická charakteristika = závislost vstupní hodnoty na výstupu
  - odezva na jednotkový skok, závislá na čase
- dynamické
  - přechodová charakteristika
    - měří se v okamžiku přivedení impulsu
  - frekvenční charakteristika

### Druhy řízení

- ovládání - bez zpětné vazby
- regulace - se zpětnou vazbou
- kybernetická zařízení - samočinné řízení

### Druhy regulace

- spojitá
- nespojitá
- na konstantní hodnotu
- programová
- vlečná

## Blokové schéma regulačního obvodu

- lednička, žehlička, vytápění, klimatizace, ...

<p align="center">
  <img src="img/13-01.png" />
</p>

- `w` ► požadovaná hodnota = nastavení požadované hodnoty
- `y` ► regulovaná veličina (např.: teplota, tlak, napětí, ...)
- `e` ► regulační odchylka = rozdíl skutečné a žádané hodnoty
- `u` ► akční veličina (např.: impuls pro sepnutí kompresoru, tepelné spirály, …)
- `d` ► poruchová veliči (např.: otevření dveří lednice)

**Výpočet regulační odchylky:** `e = w - y`

## Regulované soustavy

### Regulovaná soustava (RS)

<p align="center">
  <img src="img/13-02.png" />
</p>

### Rozdělení RS

Regulovaná veličina - rychlost, otáčky, tlak, síla, teplota, výška hladiny, intenzita světla,
chemické složení, ...

#### Zda se regulovaná veličina/y ustálí:

- statické - `y` se ustálí (př.: nenucený odtok/přítok)
- astatické - `y` kolísá (stoupá nebo klesá) (př.: nenucený odtok/přítok)

#### Dle počtu kapacit:

- **jednokapacitní**
  - př. kompresor o jedné nádobě na stlačený vzduch (regulace výšky hladině v nádrži / tlaku v tlakové nádobě)
- **dvoukapacitní** - nejčastější
  - př.: dvě nádrže v sérii (za sebou) při regulaci tlaku
- **vícekapacitní**
- **bezkapacitní**
  - př.: krátký úsek potrubí
- **s dopravním zpožděním**
  - př.: dlouhý úsek potrubí
  - pzn.: kapacita = množství energie, které je vedení schopno pojmout

### Přechodová char. 2 kapacitní statické RS (soustava 2. řádu)

<p align="center">
  <img src="img/13-03.png" />
</p>

- `I` ► inflexní bod (= místo, kde se zakřivení křivky mění)
- T<sub>u</sub> ► doba průtahu
- T<sub>n</sub> ► doba náběhu

#### Vzorce

- T<sub>p</sub> = T<sub>u</sub> + T<sub>n</sub>
- r = T<sub>u</sub> / T<sub>n</sub>

&nbsp;

- T<sub>p</sub> ► doba přechodu
- r ► regulovatelnost

## Regulátory

<p align="center">
  <img src="img/13-04.png" />
</p>

### Rozdělení regulátorů

#### 1. spojité - udržují regulovanou veličinu na požadované hodnotě

- **a. Proporcionální**
  - **nezávislý** na čase
  - parametry nastavujeme hodnotou odporu
  - **Výhody:** regulační pochod stabilizuje a zesiluje
  - **Nevýhody:** pracuje s trvalou regulační odchylkou
- **b. Integrační**
  - je závislý na čase
  - odstraňuje problém s trvalou regulační odchylkou
- **c. Derivační**
  - urychluje a stabilizuje celý regulační proces
  - reaguje pouze na změnu regulační odchylky

#### 2. nespojité - regulační veličina stále kmitá

- 2 polohové, 3+ polohové
- levné, konstrukčně jednoduché
- **Využití:** kompresor, lednice, žehlička

#### 3. sdružené

- PI, PD, PID

### Spojité regulátory - přechodová charakteristika

<table>
  <tbody>
    <tr>
      <th>Regulátor</th>
      <th align="center">Přechodová charakteristika</th>
      <th>&nbsp;</th>
    </tr>
    <tr>
      <td>
        <b>P regulátor</b><br>
        Vzorce:
        <pre><code>K<sub>r</sub> = R<sub>2</sub> / R<sub>1</sub></code></pre>
        <pre><code>u = -K<sub>r</sub> * e</sub></code>
      </td>
      <td align="center"><img src="img/13-05.png" /></td>
      <td>K<sub>r</sub> ► součinitel přenosu (zesílení regulátoru), nastavuje se pomocí odporu</td>
    </tr>
    <tr>
      <td>
        <b>I regulátor</b><br>
        Vzorce:
        <pre><code>T<sub>i</sub> = C<sub>i</sub> / R<sub>i</sub></code></pre>
        <pre><code>u = -K<sub>r</sub> / T<sub>i</sub> ∫ e dt</code></pre>
      </td>
      <td align="center"><img src="img/13-06.png" /></td>
      <td>T<sub>i</sub> ► integrační časová konstanta</td>
    </tr>
    <tr>
      <td>
        <b>D regulátor</b><br>
        Vzorce:
        <pre><code>u = T<sub>d</sub> * K<sub>r</sub> * e<sup>'</sup></code></pre>
      </td>
      <td align="center"><img src="img/13-07.png" /></td>
      <td>T<sub>d</sub> ► derivační časová konstanta<br />e<sup>'</sup> ► rychlost změny vstupní veličiny</td>
    </tr>
  </tbody>
</table>

### Nespojitý regulátor - statická charakteristika

<p align="center">
  <img src="img/13-08.png" />
</p>

- h ► hystereze (nastavuje se tuhostí pružiny, sílou magnetu)
- w ► požadovaná hodnota
- w<sub>1</sub> ► dolní hranice
- w<sub>2</sub> ► horní hranice

## Regulační pochod

- Regulační pochod ► průběh regulované veličiny (y)

### Druhy regulačních pochodů se spojitými regulátory

#### 1. změna řídící / požadované veličiny (w)

<p align="center">
  <img src="img/13-09.png" />
</p>

- ∆Y<sub>m</sub> ► maximální překmit
- Y<sub>m</sub> ► maximální hodnota
- t<sub>0</sub> ► doba odezvy
- t<sub>R</sub> ► doba regulace

#### 2. změna poruchové veličiny (d)

<p align="center">
  <img src="img/13-10.png" />
</p>

### Druhy regulačních pochodů s nespojitými regulátory

<i>viz nespojitý regulátor</i>

<p align="center">
  <img src="img/13-11.png" />
</p>

### Kvalitu regulačního pochodu posuzujeme pomocí:

- maximálního překmitů
- doby odezvy
- doby regulace
- počtu překmitů
- regulační plochou
