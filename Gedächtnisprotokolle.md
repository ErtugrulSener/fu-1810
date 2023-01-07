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
Eine kontextfreie Grammatik besteht aus dem Quintupel:
- Startwort S
- Nichtterminale N
- Terminale T
- Produktionsregeln (N x T)