# Probleem Oplossend Denken I

## Hoofdstuk 1

* De sequentie
* De Selectie
* De Iteratie

**Algoritme: De Sequentie**

---

```pascal
opdracht 1
opdracht 2
opdracht n
```

Voorbeeld: **Algoritme** Bereken BMI

```pascal
VOERUIT(scherm, "geef lengte in meter: ")
VOERIN(klavier, lengte)
VOERUIT(scherm, "geef gewicht in kilo: ")
VOERIN(klavier, gewicht)
bodyMassIndex <- gewicht/(lengte . lengte)
RETOUR bodyMassIndex
```

**Algoritme: De Selectie**

---

```pascal
ALS voorwaarde DAN
	component1
ANDERS
	component2
EINDE ALS
```

**De eenzijdige Selectie:**

```pascal
ALS voorwaarde DAN
	component1
EINDE ALS
```

Voorbeeld: **Algoritme** Evalueer BMI.

```pascal
VOERUIT(scherm, "Geef BMI:")
VOERIN(klavier, bodyMassIndex)
ALS ((18,5 ≤ bodyMassIndex) EN (bodyMassIndex ≤ 25)) DAN
	VOERUIT(scherm, "Gezond")
ANDERS
	VOERUIT(scherm, "Risico")
EINDE ALS
```

**De Geneste selectiestructuur:**

```pascal
VOERUIT(scherm, "Geef BMI:")
VOERIN(klavier, bodyMassIndex)
ALS bodyMassIndex < 18,5 DAN
	VOERUIT(scherm, "Risico voor ondergewicht")
ANDERS
	ALS bodyMassIndex > 25 DAN
		VOERUIT(scherm, "Risico voor obesitas")
	ANDERS
		VOERUIT(scherm, "Gezond")
	EINDE ALS
EINDE ALS
```

**Algoritme: De iteratie**

---

```pascal
ZOLANG iteratievoorwaarde DOE
	iteratiecomponent
EINDE ZOLANG
```

> Er is geen do-while lus!

Voorbeeld: **Algoritme** Som van de eerste 10 strikt positieve gehele getallen.

Via `while` lus.

```pascal
i <- 1
som <- 0
ZOLANG i ≤ 10 DOE
	som <- som + i
	i <- i + 1
EINDE ZOLANG
VOERUIT(scherm, "som = " som)
```
Alternatief (for-loop):

> `i` moet niet verhoogd worden in deze lus.

```pascal
som <- 0
VOOR i = 1 TOT 10 DOE
	som <- som + i
EINDE VOOR
VOERUIT(scherm, "som = " som)
```

Met Stappen:

```pascal
som <- 0
VOOR i = 1 TOT 10 STAP 2 DOE
	som <- som + i
EINDE VOOR
VOERUIT(scherm, "som = " som)
```

### Methodes

**Sjabloon**

```pascal
naamAlgoritme (I: ...): ...
	* Preconditie: ...
	* Postconditie: ...
	* Gebruikt: ...
BEGIN
	1: ...
EINDE
```

Voorbeeld: Wat is het grootste getal?

```pascal
bepaalMaximum (I: a, b, c: gehele getallen): x: geheel getal
	* Preconditie: a, b en c zijn drie gehele getallen.
	* Postconditie: het maximum van drie getallen werd bepaald.
	* Gebruikt: /
BEGIN
	x <- a
	ALS (b > x) DAN
		x <- b
	EINDE ALS
	ALS (c > x) DAN
		x <- c
	EINDE ALS
	RETOUR X
EIND
```

Voorbeeld: Bepaal het aantal priemgetallen kleiner dan n.

```pascal
telPriemgetallen (I: n: geheel getal) : aantal: geheel getal
	* Preconditie: n is een natuurlijk getal.
	* Postconditie: het aantal priemgetallen kleiner dan n werd geretourneerd.
	* Gebruikt: /
BEGIN
	aantal <- 0
	p <- 2
	ZOLANG (p < n) DOE
		deler <- 2
		ZOLANG ((deler < p) EN (p MOD deler ≠ 0)) DOE
			deler <- deler + 1
		EINDE ZOLANG
		ALS (deler = p) DAN
			antal <- aantal + 1
		EINDE ALS
		p <- p + 1
	EINDE ZOLANG
	RETOUR aantal
EINDE
```

> Waarom tot vierkantswortel van n lopen:
>
> Stel n = n<sub>1</sub> x n<sub>2</sub>
>
> dan n<sub>1</sub> ≤ √n of n<sub>2</sub> ≤ √n
>
> Bewijs
>
> Stel n<sub>1</sub> > √n en n<sub>2</sub> > √n
>
> n = n<sub>1</sub> x n<sub>2</sub> > √n x √n = n
>
> Dus, n > n, kan niet = contradictie

### Methode 2: De zeef van Eratosthenes

***2*** ***3*** 4 ***5*** 6 ***7*** 8 9 10 ***11*** 12 ***13*** 14 15 16 ***17*** 18 ***19*** 20 21 22 ***23*** 24 25 26 27 28 ***29***

```pascal
telPriemgetallenEratosthenes (I: n: geheel getal) : aantal: geheel getal
	* Preconditie: n is een natuurlijk getal.
	* Postconditie: het aantal priemgetallen kleiner dan n werd geretourneerd.
	* Gebruikt: /
BEGIN
	noteer de rij van natuurlijk getallen 2, 3, ..., n - 1
	p <- 2
	aantal <- 0
	ZOLANG (p < n) DOE
		schrap in de rij van getallen alle veelvouden van p
		aantal <- aantal + 1
		ALS alle elementen uit de rij zijn geschrapt DAN
			p <- n
		ANDERS
			p <- het eerste niet geschrapte element
		EINDE ALS
	EINDE ZOLANG
	RETOUR aantal
EINDE
```

## Hoofdstuk 2

> De tijd is rechtevenredig met het aantal instructies die uitgevoerd worden.
>
> We nemen aan dat alle basis instructies even lang duren, bijvoorbeeld: optelling, aftrekken, deling, vermenigvuldiging, ...

### Het aantal instructies exact gaan tellen.

#### Voorbeeld 1:

```pascal
BEGIN
    kwadraat <- n . n
    RETOUR (kwadraat)
EINDE
```

| &nbsp;            | # instructies | # keer | totaal |
| ----------------- | :-----------: | :----: | :----: |
| kwadraat <- n x n | 2             | 1      | 2      |
| RETOUR(kwadraat)  | 1             | 1      | 1      |
| &nbsp;            | &nbsp;        | &nbsp; | 3      |

`T(n)` = 3

#### Voorbeeld 2:

```pascal
BEGIN
    som <- 0
    VOOR i = 1 TOT n DOE
        som <- som + i . i
    EINDE VOOR
    RETOUR (som)
EINDE
```

| &nbsp;                                     | # instructies | # keer | totaal |
| ------------------------------------------ | :-----------: | :----: | :----: |
| som <- 0                                   | 1             | 1      | 1      |
| VOOR i = 1 TOT n DOE                       | 2             | n + 1  | 2n + 2 |
| &emsp;som <- som + i . i | 3             | n      | 3n     |
| EINDE VOOR                                 | &nbsp;        | &nbsp; | &nbsp; |
| RETOUR (som)                               | 1             | 1      | 1      |
| &nbsp;                                     | &nbsp;        | &nbsp; | 5n + 4 |

`T(n) = 5n + 4`

> Een `VOOR` lus heeft altijd 2 instructies.


#### Voorbeeld 3:

```pascal
BEGIN
    grootste <- 0
    VOOR i = 0 TOT n - 1 DOE
        ALS a[i] < grootste DAN
            grootste <- a[i]
        EINDE ALS
    EINDE VOOR
    RETOUR (grootste)
EINDE
```

| &nbsp;                          | # instructies | # keer | totaal       |
| ------------------------------- | :-----------: | :----: | :----------: |
| grootste <- 0                   | 1             | 1      | 1            |
| VOOR i = 0 TOT n - 1 DOE        | 2             | n + 1  | 2n + 2       |
| &emsp;ALS a[i] < grootste DAN   | **1** c       | &nbsp; | &nbsp;       |
| &emsp;&emsp;grootste <- a[i]    | **1** c       | n      | cn           |
| &emsp;EINDE ALS                 | &nbsp;        | &nbsp; | &nbsp;       |
| EINDE VOOR                      | &nbsp;        | &nbsp; | &nbsp;       |
| RETOUR (grootste)               | 1             | 1      | 1            |
| &nbsp;                          | &nbsp;        | &nbsp; | (2 + c)n + 4 |

`T(n) = (2 + c)n + 4`


#### Voorbeeld 4:

```pascal
BEGIN
    som <- 0
    VOOR i = 0 TOT n DOE
        VOOR j = 1 TOT n DOE
            som <- som + i . j
        EINDE VOOR
    EINDE VOOR
    RETOUR (som)
EINDE
```

| &nbsp;                          | # instructies | # keer        | totaal                  |
| ------------------------------- | :-----------: | :-----------: | :---------------------: |
| som <- 0                        | 1             | 1             | 1                       |
| VOOR i = 0 TOT n DOE            | 2             | n + 1         | 2n + 2                  |
| &emsp;VOOR j = 1 TOT n DOE      | 2             | (n + 1)n      | 2n<sup>2</sup> + 2n     |
| &emsp;&emsp;som <- som + i . j  | 3             | n<sup>2</sup> | 3n<sup>2</sup>          |
| &emsp;EINDE VOOR                | &nbsp;        | &nbsp;        | &nbsp;                  |
| EINDE VOOR                      | &nbsp;        | &nbsp;        | &nbsp;                  |
| RETOUR (grootste)               | 1             | 1             | 1                       |
| &nbsp;                          | &nbsp;        | &nbsp;        | 5n<sup>2</sup> + 4n + 4 |

`T(n) = 5n<sup>2</sup> + 4n + 4`


### &Theta; notatie

> **EXAMEN:** bepaal theta notatie. (Big &Theta; Notation).

![](http://d.pr/i/12eU6+)

![](http://d.pr/i/up9m+)