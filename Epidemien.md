# Epidemien

Hierbei geht es um die Modellierung der Ausbreitung von ansteckenden Krankheiten.
Zentral sind dabei:
- SIR-Modelle: Teilt die Bevölkerung in drei Gruppen:
    - **S**usceptible (Anfällige)
    - **I**nfected (Infizierte)
    - **R**esistant (Immune/Genesene)
- Berechnung von:
    - Infektionsraten
    - Genesungsraten
    - Sterberaten
    - Geburtenraten
- Berücksichtigung verschiedener Bevölkerungsgruppen möglich

## Logistisches Modell
Für die Entwicklung eines Modells zur Ausbreitung von ansteckenden Krankheiten treffen wir zunächst einfache Annahmen, die uns zur bereits bekannten logistischen Gleichung führen.
**Grundannahme:** In einer Population der Größe $N$ beginnt zum Zeitpunkt $t₀ = 0$ der Ausbruch einer ansteckenden Krankheit. Wir untersuchen die Ausbreitung dieser Krankheit unter folgenden Annahmen:
- jedes Mitglied der Population kann infiziert werden
- im untersuchten Zeitraum gibt es keine Heilung von der Krankheit
- jede infizierte Person ist ansteckend, kann sich frei bewegen und Kontakt zu anderen Mitgliedern haben
- in jeder Zeiteinheit hat jede infizierte Person $k$ Kontakte mit anderen Mitgliedern, und jeder Kontakt mit einer gesunden Person führt zur Infektion dieser Person

Aus diesen Annahmen können wir die Anzahl der Kontakte und die Änderungsrate der infizierten Personen $I(t)$ für einen kurzen Zeitraum $Δt$ wie folgt ableiten:
- Anzahl der Kontakte eines Mitglieds mit gesunden Personen: $Q(t) = Δt k (N-I(t))/N$
- Anzahl der Kontakte aller infizierten Personen mit gesunden Personen: $Q(t) I(t)$
- Änderungsrate der infizierten Personen: $dI/dt = k I(t) (N - I(t))/N$
das heißt: $dI/dt = k I(t) - (k/N) I²(t)$

$dI/dt$ ...  Änderungsrate der Infizierten
$N$ ... Gesamtpopulation
$I(t)$ ... Anzahl der Infizierten zum Zeitpunkt t
$k$ ... Kontaktrate

## SIR Modelle

Da die Dynamik der Ausbreitung einer ansteckenden Krankheit von vielen weiteren Faktoren abhängig sein kann, gibt es einen differenzierteren Satz von Modellen: SIR-Modelle, die die Wechselwirkungen berücksichtigen und den Verlauf von anfälligen (Susceptible), infizierten (Infected) und resistenten (Resistant) Personen beschreiben.

Es gelten folgende Annahmen:
- Eine Infektion erfolgt durch den Kontakt eines Gesunden mit einer infizierten Person
- Es werden keine Latenzzeiten berücksichtigt, d.h. eine infizierte Person ist sofort ansteckend
- Eine genesene Person ist dauerhaft immun gegen die Krankheit
- Berücksichtigung von Geburts- und Sterberaten in der Gesamtpopulation
- Jedes neugeborene Kind ist entweder anfällig oder immun (durch Impfung oder Veranlagung)

<br>

Wenn wir den Beginn der Epidemie zum Zeitpunkt $t = 0$ in einer Population mit $N$ Mitgliedern annehmen, dann werden die Zusammenhänge zwischen den drei getrennten Teilmengen der Population ($S$, $I$ und $R$) wie folgt berechnet:
- Anzahl der Anfälligen ($S$) (die nach Kontakt mit Infizierten infiziert werden) zum Zeitpunkt $t$ ... $S(t)$
- Anzahl der Infizierten ($I$) (infizierte Personen können Anfällige infizieren) zum Zeitpunkt $t$ ... $I(t)$
- Anzahl der resistenten Mitglieder ($R$) (sicher vor Infektion) zum Zeitpunkt $t$ ... $R(t)$
- Anfangsbedingungen: $S(0) = S_0$, $I(0) = I_0$, $R(0) = R_0$
- Konstante Populationsgröße zu allen Zeitpunkten $t$ ... $S(t) + I(t) + R(t) = S_0 + I_0 + R_0 = N$

<br>

Wenn wir den Beginn der Epidemie zum Zeitpunkt $t = 0$ in einer Population mit $N$ Mitgliedern annehmen, dann werden die Zusammenhänge zwischen den drei getrennten Teilmengen der Population ($S$, $I$ und $R$) wie folgt berechnet:

**Übergangs-/Änderungsraten:**
- Infektionsrate: $α S(t) I(t) / N$ mit $α>0$
- Genesungsrate: $β I(t)$, $β>0$
- Berücksichtigung von Geburts- und Sterberate $μ, \ N$
- Berücksichtigung der Immunisierung als Ergebnis der Impfung von Neugeborenen

Bedeutung der Parameter:
- $α$ ... beschreibt, wie schnell sich die Krankheit ausbreitet
- $β$ ... zeigt an, wie schnell Infizierte genesen
- $μ$ ... berücksichtigt demografische Veränderungen (Geburts-/Sterberate)
- $p$ ... ist der Anteil der Neugeborenen, die immunisiert sind 
<br>

Wenn wir diese Überlegungen zusammenfassen, erhalten wir folgendes System von Differentialgleichungen:

```math
S'(t) = μ (1 - p) N - α S(t) I(t) / N - μ S(t) \\
I'(t) = α S(t) I(t) / N - β I(t) - μ I(t) \\
R'(t) = μ p N + β I(t) - μ R(t)
```

![SIR-Flowchart](img/SIRFlowchart.png)

## SIR-Modelle - Epidemie ohne demografische Prozesse

Für die Analyse von Epidemien über einen kurzen Zeitraum werden demographische Effekte von Geburten und Todesfällen vernachlässigt.
Ein einfacheres Modell ergibt sich durch Setzen von $μ = 0$:
```math
S'(t) = -α S(t) I(t) / N \\
I'(t) = α S(t) I(t) / N - β I(t) \\
R'(t) = β I(t)
```

Wenn wir statt der absoluten Zahlen die Verhältnisse zur Gesamtpopulation $N$ betrachten ($s(t) = S(t)/N, \ i(t) = I(t)/N, \ r(t) = R(t)/N$), erhalten wir Werte im Intervall $[0,1]$:
```math
s'(t) = -α s(t) i(t) \\
i'(t) = α s(t) i(t) - β i(t) \\
r'(t) = β i(t)
```
Das ist ein vereinfachtes Modell für kurzfristige Betrachtungen, bei dem:
- Geburten und Todesfälle ignoriert werden
- nur die relativen Anteile der Gruppen betrachtet werden
- die Summe $s(t) + i(t) + r(t) = 1$ konstant bleibt

<br>

Wenn eine infizierte Person in eine vollständig anfällige Population kommt, können wir analysieren, unter welchen Bedingungen eine Epidemie ausbrechen kann und welcher Anteil der Population betroffen sein wird.

Durch die Analyse der Startphase des zuvor gegebenen Modells sehen wir, dass der Anteil der Infektionen $i(t)$ nur dann ansteigt, wenn die Infektionsrate $(α s(t) i(t) - β i(t))$ zum Zeitpunkt $t = 0$ größer als $0$ ist.

Zu Beginn ist fast die gesamte Population anfällig, sodass wir $s(t) ≈ 1$ haben → daraus ergibt sich die Ungleichungsbedingung $(α - β > 0)$ oder $(α/β > 1)$.
Mit anderen Worten:
- Eine Epidemie kann nur ausbrechen, wenn die Infektionsrate $α$ größer ist als die Genesungsrate $β$
- Das Verhältnis $α/β$ muss größer als $1$ sein
- Das ist ein kritischer Schwellenwert für den Ausbruch einer Epidemie

<br>

Das Verhältnis $α/β$ gibt an, wie viele neue Infektionen ein erster Infizierter während seiner Infektionsperiode verursacht.
- $R₀ = α/β$ ... "Basisreproduktionszahl"

Diese charakteristische Zahl sagt uns, ob eine Epidemie ausbrechen wird oder nicht.

<br>

Die mathematische Analyse dieses Differentialgleichungssystems kann numerisch oder durch Berechnung der Trajektorie in der $(s, i)$-Phasenebene erfolgen. In jedem Fall hat $r(t)$ keinen Einfluss auf die ersten beiden Gleichungen und kann daher separat analysiert werden.
$r(t)$ ist das Integral von $β i(t)$ über die analysierte Zeit $(0,t)$.

Die Trajektorie in der $(s,i)$-Phasenebene kann als explizite Funktion $i = i(s)$ formuliert werden, indem man folgende Differentialgleichung löst (die sich aus der Division der beiden bereits bekannten Differentialgleichungen ergibt):
```math
i'(t)/s'(t) = i'(s) = (α s i - β i)/(-α s i) = -1 + σ/s \\
i(s) = (s₀+i₀) - s + σ log(s/s₀)
```
- $σ$ ist dabei der Kehrwert der Basis-Reproduktionszahl $(σ = 1/R₀)$ ... also $σ = β/α$

![SIR Phasen-Plot](img/SIRPhasenPlot.png)

- Je kleiner $σ$ (also je größer $R₀$), desto höher ist der maximale Anteil der gleichzeitig Infizierten
Alle Kurven zeigen einen typischen Verlauf

- Erst Anstieg bis zum Maximum
- Dann Abfall der Infektionen
- Schließlich Erreichen eines Endpunkts, bei dem noch ein Teil der Population anfällig bleibt

Das beschreibt den typischen Verlauf einer Epidemie mit einem Peak und anschließendem Abklingen, auch wenn nicht alle anfälligen Personen infiziert werden.

Wenn es während der Analyse einer Epidemie signifikante Todesfälle gibt, dann können diese als resistente Mitglieder gezählt werden. Dadurch wird die Gesamtgröße der Population konstant gehalten, ohne demografische Veränderungen explizit zu berücksichtigen.