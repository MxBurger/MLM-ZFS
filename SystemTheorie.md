# System-Theorie-Basics

## Aspekte der System-Theorie
![System-Theorie](img/SystemTheorie.svg)
Im allgemeinen Fall werden die Inputs nicht von den Interaktionen der Komponenten beeinflusst.

Mathematisch wird ein allgemeines dynamisches System als 6-Tupel formuliert:
$S=(T, A, B, Q, \delta, \lambda)$ (System, Automat)
- $T$ Zeitdomäne (Zeitbereich)
- $A$ Eingangsdomäne (Eingangsbereich)
- $B$ Ausgangsdomäne (Ausgangsbereich)
- $Q$ Zustands-Menge
- $\delta : Q \times A \rightarrow Q$ globale Zustandsübergangsfunktion
- $\lambda : Q \times B \rightarrow Q$ Ausgabefunktion

Die Zustandsübergangsfunktion $\delta$ definiert, wie sich der Systemzustand basierend auf dem aktuellen Zustand und Eingang ändert. Die Ausgabefunktion $\lambda$ bestimmt, welche Ausgabe das System bei gegebenem Zustand und Eingang erzeugt.

