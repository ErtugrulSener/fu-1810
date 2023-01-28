## Welche Phasen hat die Übersetzung? (1)
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

## Welche Aufgabe hat die lexikalische Analyse?
Das erkennen von Token in einem Zeichenstrom anhand von regulären Ausdrücken. Für eine Programmiersprache also sowas wie:

- if, begin while (Wortsymbole)
- Variablennamen
- numerische Konstanten

## Was ist ein regulärer Ausdruck?
Zeichenketten auf Basis syntaktischer Regeln, die es ermöglichen, Zeichenfolgen zu beschreiben. Sie beschreiben damit formal reguläre Sprachen.

## Zwischendurch habe ich die Handimplementierung eines Scanners auf Basis von Zustandsdiagrammen (NEAs) erläutert.
Frage, wie geht das?

## Welche Aufgabe hat die Syntaxanalyse?
Aufgabe der Syntaxanalyse ist es, hierarchische Strukturen in Programmen (oder anderen Texten) zu erkennen. Diese Strukturen lassen sich nicht mehr mir regulären Ausdrücken beschreiben, wohl aber mit kontextfreien Grammatiken.

Beispiele:
- Arithmetische Ausdrücke
- Bedingte Anweisungen
- Schleifen
- Prozedurdeklarationen

Eingabe der Syntakanalyse ist die Tokenfolge, Ausgabe ist ein Syntaxbaum.

## Was ist eine reguläre Sprache? Meinerseits verweise auf die induktive Definitionen. 
Eien reguläre Sprache wird induktiv definiert anhand folgender Regeln:

1. Das leere Wort und die leere Menge {$\epsilon$} sind reguläre Sprachen.
2. Für jedes a € $\Sigma$ ist {a} eine reguläre Sprache.
3. Wenn R und S reguläre Sprachen sind, dann sind auch R $\cup$ S, RS und R* reguläre Sprachen.
4. Nichts sonst ist eine reguläre Sprache über $\Sigma$.

## Welche Arten der Syntaxanalyse gibt es? Top Down Bottom Up. Bisschen die Unterschiede erklärt. (1)
![[Gedächtnisprotokolle_Güting#Syntaxanalyse: Welche Verfahren gibt es? (3)]]

## Was setzt jede Variante der Top-down-Analyse voraus?
Frage: Das man eine kontextfreie Grammatik hat, bei der keine Linkrekursionen vorkommen?

## Wodurch wird vorausschauende sackgassenfreie Analyse möglich?
Durch eine LL(1)-Grammatik, so ist es möglich auf jede Folge von Symbol (im Stack) und Terminal (in Eingabefolge) eine Produktionsregel zur Ableitung auszuwählen.

Dabei muss die Grammatik unter umständen umgeformt werden, um Linksrekursionen zu vermeiden oder um sicherzustellen, dass die Steuermenge der Alternativen in Produktionen disjunkt sind.

## Welche Verfahren gibt es bei der Bottom-up-Analyse? Welche Parser sind mächtiger? (1)
Shift-Reduce-Parser:
- Operator-Vorrangmethode

LR-Parser
- *SLR-Verfahren* (Kanonische LR(0)-Kollektion berechnen)
- *Kanonische LR-Parser* (FOLLOW Mengen des gerade erreichen Zustands berechnen, verhindert Reduce/Reduce Konflikte, man nutzt LR(1)-Elemente)
- *LALR-Parser* (Merge von gleichen Zuständen von kanonischen LR-Parsern, Verbessertes Verfahren um LALR(1)-Tabelle zu bestimmen, ohne kanonische LR(0)-Kollektion zu bestimmen)

## Warum parst man mit kontextfreien Sprachen?
Frage: Warum? Weil Reg Ex nicht alle Strukturen abbilden kann?
Oder bezieht sich die Frage hier auf kontextsensitive Sprachen?

## Sind alle Programmiersprachen kontextfrei,- (nein kontextsensitiv, Behelf mit attributierter Grammatik).

## Beschreiben Sie die LR-Analyse.
Bei der LR-Analyse kommen LR-Parser zur Nutzung. Sie gehören zur mächtigsten Klasse von Shift-Reduce-Parsern. LR-Parser liest von links nach rechts und erkennt eine Rechtsableitung (in umgekehrter Reihenfolge).

Es gibt verschiedene Methoden, um die Tabelle (mit Action und Goto) zu konstruieren (SLR, kanonische LR, LALR), grundsätzlich unterscheidet sich der LR-Parser vom Shift-Reduce-Parser aber an den auf dem Stack verwalteten Informationen und der Struktur der Analysetabelle.

Auf dem Stack wird eine alternierende Folge verwaltet, das aus Grammatiksymbolen und Zuständen besteht. Theoretisch bräuchte man sogar nur die Zustände.

## Warum gibt es neben der syntaktischen noch die semantische Analyse?
Das Ergebnis der Syntaxanalyse ist ein Syntaxbaum. Das nächste Ziel ist es, aus dem gegebenen Baum Programme der Zielsprache der Übersetzung zu generieren.

In der Praxis werden Übersetzungsschritte verzahnt durchgeführt, sobald Teilstrukturen des Ableitungsbaums erkannt sind, es muss nicht der gesamte Baum aufgebaut werden.

## Was ist eine attributierte Grammatik?
![[ke04#Lehrziel-Fragen#attributierte Grammatik]]

## Wozu braucht man Symboltabellen?
Symboltabellen enthalten wichtige Informationen, die zur Phasen der Optimierung und Codeerzeugung zur Verfügung stehen.

Zur Laufzeit benötigt das Programm diese Informationen nicht mehr.

## Welche Codeoptimierungsverfahren gibt es? Nach der Aufzählung von allen im Kurstext genannten, sollte ich einige davon aussuchen und genauer erläutern.
Maschinenunabhängige Optimierung:
- lokale Optimierung
	- Konstantenpropagation und Konstantenfaltung
	- Kopierpropagation
	- Reduktion der Stärke von Operatoren
	- In-Line Expansion
	- Elimination redundanter Berechnungen

- Schleifenoptimierung
	- Verlagerung von Schleifeninvarianten
	- Vereinfachung von Berechnungen mit Schleifenvariablen
	- Schleifenentfaltung

- globale Optimierung
	- Eliminiation toten Codes
	- Code Hoisting

Maschinenabhängige Optimierung:
- Anweisungsreihenfolge und Registerauswahl
- Befehlsauswahl
- Peephole Opimization

## Wieso sind Programmiersprachen nicht regulär?
Weil sich nicht jede Programmiersprache (oder vermutlich die Wenigsten) durch einen regulären Ausdruck beschreiben lassen. Auch wenn die Sprache sehr regelmäßig aufgebaut ist, bedeutet das nicht, dass sie regulär ist.

## Kann jede Programmiersprache auf Basis von kontextfreien Grammatiken übersetzt werden? (Das wusste ich nicht so genau. Hab gesagt nein und das war auch richtig. Siehe semantische Phase!)
Nein?
Frage: Aber warum

## Was ist eine attributierte Grammatik?
Hier hing er dann weiter an der Frage zu welcher Sprachklasse die denn gehören? Das einzige was mir einfiel was höher war als kontextfrei waren von Turing Maschinen erkennbare. War aber falsch: Kontextsensitive Sprache(Also die von Turing Maschinen erkennbaren mit beschränkten Band glaub ich)

## Wofür brauchen wir die Attribute?
Hab gesagt um z.B Typdefinition von Bezeichnern zu merken. Auch weil die eventuell später überprüft werden. Das war in Ansätzen das was er wollte, aber er hat mir da eine ganze Weile (bestimmt mehrere Minuten) noch etwas erklärt über Typdefinition etwa in der Richtung von dem hier bei 
Wiki:“Eine Attributgrammatik ist eine kontextfreie Grammatik, die um Attribute sowie Regeln und Bedingungen erweitert ist. Angewandt wird das Konzept im Compilerbau, um beispielsweise die Einhaltung von Regeln zu überprüfen, die mit kontextfreien Grammatiken nicht formuliert werden können. Solche Regeln sind z. B. die, dass jede Variable deklariert sein muss und ihrem Datentyp entsprechend verwendet wird“ Im Nachhinein hat er auch angemerkt, dass der Teil der Semantikanalyse wohl mein Schwachpunkt war.

## Welchen ZC kennen Sie? Hab 3AC genannt und kurz was dazu gesagt
3AC - Jeder Befehl besitzt hier maximal 3 Argumente

```C
x := a + b
```

Die Argumente sind dabei (Adressen von) Variablen oder Konstanten.
Außerdem können Befehle mit Sprungmarken versehen werden. Beispiel:

```C
L1: x := y[i]
```

## Jeweils n Beispiel für eine Optimierung 
Algebraische: Hab gesagt Zusammenfassung von arithmetischen Ausdrücken
Maschinenunabhängige: Z.B Löschen von nicht verwendeten Variablen! Prozessorspezifisch: Fiel mir nichts ein, er schlug Registerallokation vor, also Anpassung an die Anzahl der Register des Prozessors z.B.
