# KE 1
## Warum übersetzt man eigentlich? (1)
Weil man etwas nur in der Quellsprache A beschreiben kann, das Zielsystem aber nur die Zielsprache B versteht. Deshalb braucht es die Übersetzung.

## Was wird alles übersetzt? (1)
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

## Was ist der Unterschied zwischen Compiler und Interpreter?
Compiler:
- übersetzt gesamte Eingabe
- Ausführung erst zu späterem Zeitpunkt
- schnelle Ausführungsgeschwindigkeit aber längere Programmentwicklung

Interpreter: 
- übersetzt kleine Teile der Eingabe (z. B. Zeilen)
- sofortige Ausführung
- schnelle Programmentwicklung, aber langsamere Ausführungsgeschwindigkeit

Mischform: Compiler übersetzt Programm in einfachen Zwischencode, der zur Laufzeit effizient von einem Interpreter verarbeitet werden kann (z. B. Java).

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

## Was sind die logischen Schritte einer Übersetzung?
2 Phasen: Analysephase und Synthesephase.
Der Übersetzungsprozess ist unterteilt in 6 Schritte.
- Lexikalische Analyse => Tokenerkennung mit Hilfe von Regulären Ausdrücken und deterministischen endlichen Automaten

- Syntaxanalyse => Erzeugen eines Syntaxbaumes mit Hilfe von KFG

- Semantische Analyse => Der Syntaxbaum wird um kontextsensitive Informationen erweitert (Typecheck, Var_Declaration)

- Zwischencodeerzeugung => Diese Phase stellt eine Art Zwischenebene zwischen Hochsprache und Maschinensprache dar. (Modularität) Hier wird eine abstrakte Maschinensprache (3-Address-Code(3AC)) erzeugt. Es wird bewusst auf Maschinenabhängigkeit verzichtet! (Einfacher)

- Codeoptimierung => Hier wird der (naiv) erzeugte 3AC optimiert. (z.B. Konstantenpropagation, Peephole, loop-Auflösung, evtl. Komplexität der Berechnungen verringern... )

- Codeerzeugung => Im letzten Schritt wird der optimierte 3AC zu Maschinenabhängigem Code generiert. Zu lösende Probleme sind u.a.: Effiziente Registerzuteilung, Operationen auf bestmögliche Befehlsfolgen abbilden. 

## Warum fasst man syntaktische und semantische Analyse nicht in einem Schritt zusammen?
Der Input für die semantische Analyse ist ein vollständiger Syntaxbaum. Um bestimmte Semantiken zu erkennen z.B: Operatorüberladung muss der gesamte Ausdruck bekannt sein, erst dann kann man daraus die Semantik erschließen.

# KE 2
## Was ist eine kontextfreie Grammatik?
Eine Kontextfreie Grammatik beschreibt kontextfreie Sprachen. Mit Hilfe der kontextfreien Grammatik lassen sich Syntaxregeln überprüfen. Es werden jeweils Produktionen anhand von Produktionsregeln erkannt und angewandt, wobei die Produktionen keine Abhängigkeiten auf der linken Seite haben dürfen (sonst sind diese kontextsensitiv), d.h. es steht nur ein Nichtterminal auf der linken Seite der Produktion.

## Definition einer kontextfreien Grammatik
Eine kontextfreie Grammatik besteht aus dem Quadrupel G = (N, $\Sigma$, P, S) wobei gillt:
- N ist ein Alphabet aus Nichtterminalen
- $\Sigma$ ist ein Alphabet von Terminalen. Die Alphabete N und $\Sigma$ sind disjunkt.
- P $\subseteq$ N x (N $\cup$ $\Sigma$)* ist eine Menge von Produktionsregeln.
- S € N ist das Startsymbol.

## Syntaxanalyse: Welche Verfahren gibt es? (1)
Allgemein: Das Ziel ist es aus einer Tokenfolge einen (abstrakten) Syntaxbaum zu erzeugen. Das geht mittels:
- Top-Down Analyse 
	- Der Syntaxbaum wird von oben nach unten erzeugt. Es werden Eingabefolgen anhand von Linksableitungen erkannt. Kann nicht mit Linksrekursionen umgehen (Grammatik muss bei Linksrekursionen erst umgeformt werden. Das geht nicht immer). Gefahr von Sackgassen und Backtracking. Deshalb LL(1) Grammatik. Generelles Vorgehen: Auf dem Stack stehen Nichtterminale. Diese werden mit den Eingabetoken vergleichen. Die Nichtterminale werden anhand der Analysetabelle so lange reduziert bis sich auf dem Stack ein Terminal gleich dem Eingabeterminal befindet. Dann wird weitergelesen. Wenn es keine passende Reduktion gibt, dann Fehler.  
- Bottom-Up Analyse 
	- Der Syntaxbaum wird von unten nach oben erzeugt. Es werden Eingabefolgen anhand von Rechtsableitungen in umgekehrter Reihenfolge erkannt. Ist mächtiger als Top Down. Kann mit Linksrekursionen umgehen. LR1 Parser: Es wird ein Det. Automat gebaut anhand von dem die Produktionen mit allen möglichen Eingabefolgen überprüft werden.  => Shift/Reduce Parser. Es werden Eingabefolgen so lange auf den Stack gelegt, bis eine Reduktion angewandt werden kann. Wenn keine Reduktion angewandt werden kann -> Fehler. 
- Allgemein: Top Down muss entscheiden welche Ableitung angewandt werden muss mit nur einem Lookahead. Der Bottom Up Parser kann diese Entscheidung treffen, nachdem er alle Eingabefolgen gesehen hat. 

## Top-Down Analyse: Welche Probleme gibt es?
Sackgasse (wenn kein Lookahead, also LL(0)), Linksrekursivität...

## Was passiert genau auf dem Stack?
Bei der Top-Down Analyse steht auf der obersten Position des Stacks die gerade betrachtete Abfolge. Wenn die Eingabefolge ein Terminal ist und auf dem Stack steht ein Nichtterminal, dann wird anhand der Analysetabelle eine passende Ableitung ausgewählt. So lange bis auf dem Stack ein Terminal gleich dem Eingabeterminal ist. Wenn Terminal_stack == Terminal_Eingabe, dann wird weitergelesen. 

Wenn es keine passende Produktion gibt (kein Eintrag in Analysetabelle) => Fehler.    

## Was ist hier eine abstrakte Maschine?
Ein Mechanismus bestehnd aus Stack, Eingabe, Analysetabelle und Ausgabe.

## Wie wird eine Analysetabelle erstellt?
Es werden die Steuermengen (FIRST und ggf. FOLLOW) und die Nummer der entsprechenden Produktionen eingetragen. In der linken Spalte sind alle Nichtterminale aufgelistet, in der "Oberen" alle Terminale.

## Was macht ein Vorgreifender Analysator?
*Analysetabelle*:
Lesen von Links nach rechts, Linksableitung anwenden mit Lookahead auf das nächste Eingabezeichen. Der Parser verwendet das aktuelle Eingabesymbol und das aktuelle Nichtterminalsymbol, um die entsprechende Produktionsregel in der Analysetabelle zu suchen. Funktioniert nur mit LL(1)-Grammatik. 

*Rekursiver Abstieg:*
Es werden nur die Steuermengen benötigt, aber keine Analysetabelle. Außerdem werden rekursive Prozeduren für jedes Nichtterminal angelegt.
Es wird am Anfang die Startprozedur aufgerufen. Der Baum ergibt sich dann aus dem rekursiven Aufruf der Prozeduren. Die Prozeduren entscheiden anhand des aktuellen Eingabetokens welche Produktion anzuwenden ist.

Falls das Eingabetoken an der Stelle nicht erwartet ist, läuft man in einen Fehler.

## Wie wird die Steuermenge bestimmt?
Dafür werden zuerst die FIRST Mengen bestimmt. Die FIRST Mengen sind alle Terminale, mit denen ein aus einem Nichtterminal abgeleiteter String beginnen kann. 

Falls ein Epsilon abgeleitet wird, werden noch die FOLLOW Mengen benötigt. Die FOLLOW Mengen sind die Terminale, die direkt nach einem Nichtterminal auf der rechten Seite stehen können.

Aus diesen Mengen zusammen wird die Steuermenge bestimmt. Falls es mehrere Produktionen für ein Nichtterminal gibt, wird die Steuermenge entsprechend aufgeteilt für jede Produktion. Es gibt eine Steuermenge je Produktion.

Voraussetzung ist, dass für jedes Nichtterminal die Steuermengen seiner Alternativen disjunkt sind, sonst ist diese Grammatik nicht vom Typ LL(1) - Es gäbe eine Mehrdeutigkeit.

## Bottom-Up Analyse: Was ist ein Shift-Reduce-Parser?
Ein Shift Reduce Parser liest die Eingabetoken ein und legt diese auf den Stack ab. Nach jedem Einlesen wird entschieden, ob es eine Produktion der eingelesenen Folge gibt. (Handle b: A -> b) Falls ja, wird reduce angewandt und es wird b durch A auf dem Stack ersetzt. Falls nein, wird geshiftet und die nächste Eingabefolge eingelesen. 

LR Parser sind die mächtigste Klasse von shift-reduce Parsern.

## Welche Probleme gibt es?
Wesentliches Problem ist es zu entscheiden, ob eine vollständige Seite reduziert werden soll oder noch nicht. => Handle erkennen.

Bei mehrdeutigen Grammatiken kann es zu Shift/Reduce Konflikten kommen. (z.B. dangling else Problem).

## Welches ist das einfachste Verfahren
Operator Vorrang-Analyse 
Wurde speziell für die Eingabe von arithmetischen Ausdrücken entwickelt und eignet sich somit nicht für beliebge Grammatiken => schwächstes Verfahren. 

Die Eingabe wird auf dem Stack abgelegt. Um zu erkennen ob shift oder reduce angewandt werden soll, werden Spitze Klammern (< >)  und ein "=" Zeichen benutzt. In einer Tabelle werden jeweils die Beziehungen, "Rangordnungen" und Prioritäten der Terminale festgelegt.  
Wenn die Beziehung zwischen dem obersten Element auf dem Stack und der Eingabe "<" oder ein "=" gilt, wird shift angewandt. Wenn die Beziehung ">" gilt, wird reduce angewandt.

## Was passiert genau auf dem Stack?
Auf dem Stack werden die Beziehungen, die reduzierten Nichtterminale und die eingelesenen Token abgelegt. Die Eingabe wird wieder so lange auf dem Stack abgelegt während die Beziehungen "<" oder "=" gelten. 

## Was ist ein Handle?
Ein Handle ist die rechte Seite einer Produktion, durch die ersetzt wird. Somit wird der Reduktionsprozess erfolgreich zuende geführt.

## Warum heißen die Parser "Shift Reduce"?
Weil das die wesentlichen Aktionen des Parsers sind (neben accept und error). Bei:

shift - wird das nächste Symbol der Eingabefolge entnommen und auf den Stack gelegt.

reduce - ein Handle $\beta$ einer Produktion $A -> \beta$ bildet das obere Ende eines Stacks. Man ersetzt $\beta$ auf dem Stack durch A.

## Warum heißt der einfachste Shift-Reduce Parser "Operrator-Vorrang"?
Sie wurde speziell für die Syntaxanalyse arithmetischer Ausdrücke entwickelt und ist das schwächste Bottom-Up-Verfahren. Für jedes Aufeinandertreffen zweier Operatoren wird ein Vorrang (anhand der Relationen) festgelegt.

## Was sind Operatoren?
Alle Terminale / Arithmetischer Operatoren? (+, -, \*, / ...)

## Was sind Relationen?
\<. - Shift
\= - Shift
\>. - Reduce

Die Spitzen Klammern zeigen die Grenzen des Handles, die Gleich-Relation zeigt die Beziehung zwischen den Symbolen innerhalb des Handles.

## Was wird alles vom Stack genommen beim Reduce?
Kommt auf die Produktion an, zu der reduziert wird (bzw. die rechte Seite der Produktion). Wenn die Produktion 4 Symbole besitzt, werden die 4 Symbole und die Relationen zwischen ihnen vom Stack genommen.

## Warum "Raten der Ableitungsregel"?

## Beispielgrammatik aufschreiben, mit der man das Erreichen einer Sackgasse demonstrieren kann.

## Aufzeichnen eines dazugehörigen Ableitungsbaumes.

## Erklären sie "Predictive Parsing".

## FIRST und FOLLOW Mengen - Was ist das?

## Wie kommt man zu einer Analysetabelle wenn man diese Mengen hat?

## Wann ist eine Grammatik nicht geeignet?