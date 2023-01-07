# Allgemeine Fragen

## Warum übersetzt man eigentlich?
Weil man etwas nur in der Quellsprache A beschreiben kann, das Zielsystem aber nur die Zielsprache B versteht. Deshalb braucht es die Übersetzung.

## Was wird alles übersetzt?
1) Höhere Programmiersprache (z.B: C++) in Maschinensprache
	- (durch Transpiler) z.B: typisierte Programmiersprache (Typescript) in andere Programmiersprache (Javascript)

2) Datenbankabfragesprachen (SQL)
	- Umwandlung der Anfrage in Operatorbaum für spätere Optimierung

3) Dokumenten Beschreibungssprachen (LaTeX, HTML)
	- *Beispiel HTML:* Browser brauchen Compilertechnik um die Struktur der Dokumente zu analysiieren

4) VLSI-Entwurfssprachen
	- steht für "Very Large-Scale Integration"
	- Beschreiben Layout elektronischer Schaltungen auf einem Chip über verscheidene Abstraktionsebenen

5) Protokolle in verteilten Sytemen
	- Austausch von Zeichenströmen über Rechnernetze
	- Struktur dieser Zeichenströme ist eine Sprache die vom Empfänger analyisiert werden muss

## Unterschiede Compiler / Interpreter
- Ein Interpreter benutzt die gleichen Analysetechniken wie ein Compiler. Sie kommen in den "ersten 3" Phasen des Übersetzerbaus zum Einsatz. (Übergeordnet "Analyse" genannt)
	- *Die 3 Phasen der Analyse sind:*
		- Lexikalische Analyse
		- Syntaxanalyse
		- Semantische Analyse

- Analyse und Ausführung laufen zeitlich verzahnt ab.

- Ein Interpreter muss z.B: bei einem FOR-Loop jedes Mal die nächsten Token erneut auswerten und das Statement ausführen.
	- Es gibt natürlich JIT - Compiler, die zur Optimierung zum Einsatz kommen, die wir hier ignorieren.
___

- Ein Compiler dagegen hat außerdem die Phasen (Übergeordnet "Synthese" genannt):
	- Erzeugen von Zwischencode
	- Codeoptimierung
	- Codeerzeugung

___

- Die folgenden Aufgaben werden parallel zu den Phasen übernommen von sowohl Interpreter als auch Compiler:
	- *Verwaltung der Symboltabelle
	- *Behandlung von Fehlern*

## Vor- und Nachteile beider Techniken
- Vorteile Interpreter:
	- Schnellere Programmentwicklung (Übersetzungsschritt entfällt, Code kann direkt ausgeführt werden)

	- Interpreter analysiert nur zur Laufzeit erreichte Teile des Programms, Compiler muss das gesamte Programm analysieren und übersetzen!
	
	- Compiler müssen dafür für jede Maschinenarchitektur standartmäßig neugeschrieben werden, weil die Zielsprache B auf jeder Architektur andere Befehle besitzen oder nicht besitzen kann.

- Nachteile Interpreter:
	- Interpreter müssen bereits analyisierte Codeschnipsel (z.B: bei Schleifen) immer wieder analyisieren, um sie auszuführen.
		- Compiler betreiben Analyseaufwand nur ein Mal

	- Es gibt beim Interpreter standartmäßig keine Codeoptimierungsphase. Daher sind interpretierte Programme meist langsamer als kompilierte.

## Definition einer kontextfreien Grammatik
Eine kontextfreie Grammatik besteht aus dem Quadrupel G = (N, $\Sigma$, P, S) wobei gillt:
- N ist ein Alphabet aus Nichtterminalen
- $\Sigma$ ist ein Alphabet von Terminalen. Die Alphabete N und $\Sigma$ sind disjunkt.
- P $\subseteq$ N x (N $\cup$ $\Sigma$)* ist eine Menge von Produktionsregeln.
- S € N ist das Startsymbol.

# Vorgehensweise eines Übersetzers

## Phasen des Übersetzerbaus
- Lexikalische Analyse
- Syntaxanalyse
- Semantische Analyse
- Erzeugen von Zwischencode
- Codeoptimierung
- Codeerzeugung

## Benennen der Eingaben und Ausgaben für die Phasen der Analyse
- Lexikalische Analyse
	- Input: Zeichenfolge
	- Output: Tokenfolge

- Syntaxanalyse
	- Input: Tokenfolge
	- Output: Syntaxbaum

- Semantische Analyse
	- Input: Syntaxbaum
	- Output: Attributierter Syntaxbaum oder AST

- Erzeugen von Zwischencode
	- Input: Attributierter Syntaxbaum oder AST
	- Output: Zwischencode

- Codeoptimierung
	- Input: Zwischencode
	- Output: Zwischencode (optimiert)

- Codeerzeugung
	- Input: Zwischencode (optimiert)
	- Output: Zielsprache / Zielcode

## Warum fasst man syntaktische und semantische Analyse nicht in einem Schritt zusammen?
Der Input für die semantische Analyse ist ein vollständiger Syntaxbaum. Um bestimmte Semantiken zu erkennen z.B: Operatorüberladung muss der gesamte Ausdruck bekannt sein, erst dann kann man daraus die Semantik erschließen.

# Parsen im Allgemeinen und Bottom-Up im Speziellen

## Wie unterscheiden sich Top-Down und Bottom-Up Parser?

## Was ist ein Handle?

## Warum heißen die Parser "Shift Reduce"?

## Warum heißt der einfachste Shift-Reduce Parser "Operrator-Vorrang"?

## Was sind Operatoren?

## Mit eigenem Beispiel eine Oeprator Vorrang Tabelle erstellen. z.B: mit den Operatoren "+" und "*".

## Was sind Relationen?

## Was wird alles vom Stack genommen beim Reduce?

# Top-Down Parser
## Warum "Raten der Ableitungsregel"?

## Beispielgrammatik aufschreiben, mit der man das Erreichen einer Sackgasse demonstrieren kann.

## Aufzeichnen eines dazugehörigen Ableitungsbaumes.

## Erklären sie "Predictive Parsing".

## FIRST und FOLLOW Mengen - Was ist das?

## Wie kommt man zu einer Analysetabelle wenn man diese Mengen hat?

## Wann ist eine Grammatik nicht geeignet?