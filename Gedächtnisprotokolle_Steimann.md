TARGET DECK: Gesprächsprotokolle_Steimann

## Welche Phasen hat die Übersetzung? (2)
Die Übersetzung hat zwei übergeordnete Phasen:
Analyse und Synthese

Zur Analyse gehören dann noch Mal feiner die Phasen:
- Lexikalische Analyse
- Syntaxanalyse
- Semantische Analyse

Zur Synthese gehören die Phasen:
- Erzeugen von Zwischencode
- Codeoptimierung
- Codeerzeugung
<!--ID: 1675153368272-->

## Welche Aufgabe hat die lexikalische Analyse?
Das erkennen von Token in einem Zeichenstrom anhand von regulären Ausdrücken. Für eine Programmiersprache also sowas wie:

- if, begin while (Wortsymbole)
- Variablennamen
- numerische Konstanten
<!--ID: 1675153368277-->

## Was ist ein regulärer Ausdruck?
Zeichenketten auf Basis syntaktischer Regeln, die es ermöglichen, Zeichenfolgen zu beschreiben. Sie beschreiben damit formal reguläre Sprachen.
<!--ID: 1675153368281-->

## Zwischendurch habe ich die Handimplementierung eines Scanners auf Basis von Zustandsdiagrammen (NEAs) erläutert.
<!--ID: 1675153368286-->

## Welche Aufgabe hat die Syntaxanalyse?
Aufgabe der Syntaxanalyse ist es, hierarchische Strukturen in Programmen (oder anderen Texten) zu erkennen. Diese Strukturen lassen sich nicht mehr mir regulären Ausdrücken beschreiben, wohl aber mit kontextfreien Grammatiken.

Beispiele:
- Arithmetische Ausdrücke
- Bedingte Anweisungen
- Schleifen
- Prozedurdeklarationen

Eingabe der Syntaxanalyse ist die Tokenfolge, Ausgabe ist ein Syntaxbaum.
Eine der Hauptaufgaben liegt darin zu überprüfen, ob die Eingabefolge (Tokenstrom) einer korrekten Syntax folgt.
<!--ID: 1675153368291-->

## Was ist eine reguläre Sprache? Meinerseits verweise auf die induktive Definitionen. 
*Skript*:
Die Menge der Zeichenketten, die auf ein Token abgebildet werden, ist die zum Ausdruck gehörige reguläre Sprache.

*Für Menschen*:
Eine reguläre Sprache ist die Menge aller Worte, die man aus einem regulären Ausdruck bilden kann.

Ein Beispiel für eine reguläre Sprache ist die Menge aller gültigen E-Mail-Adressen.
<!--ID: 1675153368295-->

---

Eine reguläre Sprache wird induktiv definiert anhand folgender Regeln:

1. Die Menge {$\epsilon$} und die leere Menge sind reguläre Sprachen.
2. Für jedes a € $\Sigma$ ist {a} eine reguläre Sprache.
3. Wenn R und S reguläre Sprachen sind, dann sind auch R $\cup$ S, RS und R* reguläre Sprachen.
4. Nichts sonst ist eine reguläre Sprache über $\Sigma$.

## Welche Arten der Syntaxanalyse gibt es? Top Down Bottom Up. Bisschen die Unterschiede erklärt. (2)
![[Gedächtnisprotokolle_Güting#Syntaxanalyse: Welche Verfahren gibt es? (4)]]
<!--ID: 1675153368301-->

## Was setzt jede Variante der Top-down-Analyse voraus?
- Eine LL(1) - Grammatik
	- Keine Linksrekursionen
	- Alle Varianten der Produktionsregeln sind disjunkt

- Linksrekursion in Rechtsrekursion überführen
S -> A
C -> d
A -> A b | C

=

S -> A
C -> d
A -> b A' | C
A' -> b A' | $\epsilon$
<!--ID: 1675153368306-->

## Wodurch wird vorausschauende sackgassenfreie Analyse möglich?
Durch eine LL(1)-Grammatik, so ist es möglich auf jede Folge von Symbol (im Stack) und Terminal (in Eingabefolge) eine Produktionsregel zur Ableitung auszuwählen.

Dabei muss die Grammatik unter Umständen umgeformt werden, um Linksrekursionen zu vermeiden oder um sicherzustellen, dass die Steuermenge der Alternativen in Produktionen disjunkt sind.
<!--ID: 1675153368311-->

## Welche Verfahren gibt es bei der Bottom-up-Analyse? Welche Parser sind mächtiger? (2)
Shift-Reduce-Parser:
- *Operator-Vorrangmethode*

LR-Parser
- *SLR-Verfahren* (Kanonische LR(0)-Kollektion berechnen)
- *Kanonische LR-Parser* (FOLLOW Mengen des gerade erreichen Zustands berechnen, verhindert Reduce/Reduce Konflikte, man nutzt LR(1)-Elemente)
- *LALR-Parser* (Merge von gleichen Zuständen von kanonischen LR-Parsern, Verbessertes Verfahren um LALR(1)-Tabelle zu bestimmen, ohne kanonische LR(1)-Kollektion zu bestimmen)
<!--ID: 1675153368317-->

## Warum parst man mit kontextfreien Grammatiken?
Zwei Dinge die mit regulären Ausdrücken nicht funktionieren:

*1)*
(((( expr ))))

*2)*
Z -> b Z
<!--ID: 1675153368327-->

## Sind alle Programmiersprachen kontextfrei,- (nein kontextsensitiv, Behelf mit attributierter Grammatik).
Nein, für die Syntaxanalyse (Syntaxbaum) reicht eine kontextfreie Grammatik. Für weitere Schritte (semantische Analyse) allerdings nicht mehr.
<!--ID: 1675153368344-->

## Beschreiben Sie die LR-Analyse.
Bei der LR-Analyse kommen LR-Parser zur Nutzung. Sie gehören zur mächtigsten Klasse von Shift-Reduce-Parsern. LR-Parser liest von links nach rechts und erkennt eine Rechtsableitung (in umgekehrter Reihenfolge).

Es gibt verschiedene Methoden, um die Tabelle (mit Action und Goto) zu konstruieren (SLR, kanonische LR, LALR), grundsätzlich unterscheidet sich der LR-Parser vom Shift-Reduce-Parser aber an den auf dem Stack verwalteten Informationen und der Struktur der Analysetabelle.

Auf dem Stack wird eine alternierende Folge verwaltet, das aus Grammatiksymbolen und Zuständen besteht. Theoretisch bräuchte man sogar nur die Zustände.
<!--ID: 1675153368349-->

## Warum gibt es neben der syntaktischen noch die semantische Analyse?
Beispiel für einen Fall, bei dem das nicht geht:

```C
func();

int func() {

};
```
<!--ID: 1675153368353-->

## Was ist eine attributierte Grammatik?
![[ke04#Lehrziel-Fragen#attributierte Grammatik]]
<!--ID: 1675153368356-->

## Wozu braucht man Symboltabellen?
Symboltabellen enthalten wichtige Informationen, die zur Phasen der Optimierung und Codeerzeugung zur Verfügung stehen.

Zur Laufzeit benötigt das Programm diese Informationen nicht mehr.
<!--ID: 1675153368361-->

## Welche Codeoptimierungsverfahren gibt es? Nach der Aufzählung von allen im Kurstext genannten, sollte ich einige davon aussuchen und genauer erläutern. (*) (2)
*Algebraische Optimierung*

*Maschinenunabhängige Optimierung:*
- *lokale Optimierung*
- Konstantenpropagation und Konstantenfaltung
```
x = 4
func(x)

// Konstantenpropagation
func(4)

---

x = 4
y = 5
z = x * y

// Konstantenfaltung
z = 20
```

- Kopierpropagation
```
x = 4
y = x
z = y * 4

// Kopierpropagation
z = x * 4
```

- Reduktion der Stärke von Operatoren
```
x**2

// Reduktion der Stärke von Operatoren
wird zu:
x*x
```

- In-Line Expansion
```
int main() {
	func(4)
}

// In-Line Expansion
int main() {
	MOV R,2
	ADD R,3
	STORE R,S
}

// Jede Funktion würde ja einen Stack aufbauen, kostet Speicher
// Sprungbefehl kostet CPU
```

- Elimination redundanter Berechnungen
```
Elimination redudanter Berechnungen
(17) t7 = i-1
(18) t8 = i-1
(19) t9 = t8 * t7

// Wegoptimieren von Zeile 18
(18) 
(19) t9 = t7 * t7
```

- *Optimierung mit Datenflussanalyse*
- *Schleifenoptimierung*
- Verlagerung von Schleifeninvarianten
```C
// Vorher:
for (int i = 0; i < 5; i++) {
	for (int j = 0; j < 5; j++) {
		int b = i * 4 + j;
	}
}

// Nachher:
for (int i = 0; i < 5; i++) {
	int temp = i * 4;
	for (int j = 0; j < 5; j++) {
		int b = temp + j;
	}
}
```

- Vereinfachung von Berechnungen mit Schleifenvariablen
```
// Siehe Skript
```

- Schleifenentfaltung
```C
// Vorher:
for (int i = 0; i < 50000; i++) {
	for (int j = 0; j < 2; j++) {
		operation(i, j);
	}
}

// Nachher:
for (int i = 0; i < 5; i++) {
	operation(i, 0);
	operation(i, 1);
}
```

- *globale Optimierung*
- Eliminiation toten Codes
```Java
// Beispiel: Variable, die nicht gebraucht wird
int a = 4;
int b = 8;

System.out.println(a);
```

- Code Hoisting
```
// Rausziehen von Teilausdrücken aus if/if-else/else Ausdrücken
// weil man sie in allen Zweigen braucht.

// Achtung: Man spart keine CPU, aber Speicher!
```

*Maschinenabhängige Optimierung:*
- Anweisungsreihenfolge und Registerauswahl
```
T1 := a+b
T2 := c+d
T3 := e-T2
T4 := T1-T3

// Man könnte T1 unmittelbar bevor T4 berechnen und damit T1 im Register halten. Man spart sich damit ein "auslagern" und "wieder holen" von T1

// Vorher:
LOAD R,a
ADD R,b
LOAD S,c s
ADD S,d
STORE R,T1
LOAD R,e
SUB R,S
LOAD S,T1
SUB S,R
STORE S,T4

// Nachher:
LOAD R,c
ADD R,d
LOAD S,e
SUB S,R
LOAD R,a
ADD R,b
SUB R,S
STORE S,T4
```

- Befehlsauswahl
```
z.B: INC i Erhöhe den Wert der Speicherzelle i um 1.

statt

LOAD R,i Lade den Wert der Speicherzelle i in Register R
ADD R,1 Addiere 1 zum Register R
STORE R,i Speichere Register R in der Speicherzelle i
```

ODER

```
Ein weiteres Beispiel für eine optimierende Befehlsauswahl ist die Ersetzung einer Integer-Multiplikation mit 2 durch einen Shift-Left-Befehl.
```

- Peephole Opimization
```
Man kann eine Schablone über die Befehlszeilen schieben und Kandidaten erkennen. Daher auch der Name "Gucklock-Optimierung".

// Beispiel:

LOAD R,y
ADD R,2
STORE R,x
LOAD R,x
MULT R,3
STORE R,z
```
<!--ID: 1675153368365-->

## Wieso sind Programmiersprachen nicht regulär?
Weil sich nicht jede Programmiersprache (oder vermutlich die Wenigsten) durch einen regulären Ausdruck beschreiben lassen. Auch wenn die Sprache sehr regelmäßig aufgebaut ist, bedeutet das nicht, dass sie regulär ist.
<!--ID: 1675153368369-->

## Kann jede Programmiersprache auf Basis von kontextfreien Grammatiken übersetzt werden? (Das wusste ich nicht so genau. Hab gesagt nein und das war auch richtig. Siehe semantische Phase!)
Für die Syntaxanalyse ja, für die semantische Analyse braucht man attributierte Grammatiken.
<!--ID: 1675153368373-->

## Was ist eine attributierte Grammatik?
*Kontextfreie Grammatiken* gehören zur Sprachklasse der kontextfreien Sprachen.

*Attributierte Grammatiken* gehören zur Sprachklasse der kontexstsensitiven Sprachen.

Eine attributierte Grammatik ist eine kontextfreie Grammatik, die um Attribute und Regeln zur Berechnung dieser Attribute (aus Attributen von in der Produktionsregeln vorkommenden Symbolen) erweitert wurde.

## Wofür brauchen wir die Attribute?
Hab gesagt um z.B Typdefinition von Bezeichnern zu merken. Auch weil die eventuell später überprüft werden. Das war in Ansätzen das was er wollte, aber er hat mir da eine ganze Weile (bestimmt mehrere Minuten) noch etwas erklärt über Typdefinition etwa in der Richtung von dem hier bei 

Wiki:“Eine Attributgrammatik ist eine kontextfreie Grammatik, die um Attribute sowie Regeln und Bedingungen erweitert ist. Angewandt wird das Konzept im Compilerbau, um beispielsweise die Einhaltung von Regeln zu überprüfen, die mit kontextfreien Grammatiken nicht formuliert werden können. Solche Regeln sind z. B. die, dass jede Variable deklariert sein muss und ihrem Datentyp entsprechend verwendet wird“ Im Nachhinein hat er auch angemerkt, dass der Teil der Semantikanalyse wohl mein Schwachpunkt war.
<!--ID: 1675153368380-->

## Welchen ZC kennen Sie? Hab 3AC genannt und kurz was dazu gesagt
- 3AC - Jeder Befehl besitzt hier maximal 3 Argumente

```C
x := a + b
```

- Postfix
- DAG
- AST

Die Argumente sind dabei (Adressen von) Variablen oder Konstanten.
Außerdem können Befehle mit Sprungmarken versehen werden. Beispiel:

```C
L1: x := y[i]
```
<!--ID: 1675153368390-->
