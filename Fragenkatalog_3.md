# Was tut ein Übersetzer?
=> kam schon

# Was übersetzt er?
=> kam schon. Sprachen, die man mit KFG ausdrücken kann?

# Welche Sprachen eignen sich als Quellsprachen? Hier wollte er die exakte Definition von kontextfreien Grammatiken haben
=> kam schon. Was ist eine KFG?

# Welche Phasen unterscheidet man?
=> kam schon. Analysephase, Synthesephase, lexikalische, syntax, semantik, Zwischencode, Optimierung, Maschinencode

# Welche Zwischensprachen kennen Sie?
3AC, Postfix Notation

# Wie wird Postfix-Notation verarbeitet? 
Es werden zuerst die Operanden und danach die ausführende Operation geschrieben. Bsp. a b c + bedeutet a = b+c
Operationen entnehmen die obersten Elemente vom Stack, führen die Operation aus und legen das Ergebnis wieder auf den Stack.

# Welche 3AC-Befehle kennen Sie? Hier sollte man wirklich alle Gruppen kennen.
=> ohje... Denke sowas kommt nicht dran...

# Welche Möglichkeiten hat man, die Top-Down-Analyse mit Vorausschau durchzuführen? 
Mit Analysetabelle und mit rekursivem Abstieg.
=> kam schon

# Wie erstellt man die Analysetabelle?
Hier wollte er auch wissen, aus was für einem Automaten man die Analysetabelle gewinnt. Bin dabei auf die Steuermengen zu sprechen gekommen. Habe die genaueDefinition aufgeschrieben.
=> Kam schon. 
Frage: Was hat es hier mit dem automaten auf sich?

# Was sind denn FIRSTk(α) und start_k? wollte er in dem Zusammenhang nochwissen
=> kam schon.

# Und wozu brauche ich bei der Definition der Steuermengen noch die FOLLOW-Mengen?
Weil es sein kann, dass man aus α ε ableiten kann

Prof. Güting zog eine vorbereitete Karteikarte hervor, auf der in etwa folgendesstand:
i1:A→α1|D 
i2:A→α2|D
Hieraus sollte ich eine Procedure in Pseudocode schreiben, die den rekursiven Abstieg implementiert.

# Welche Arten von Grundsymbolen hat eine Programmiersprache üblicherweise?
??? Terminale? id, if, else, while, for, return...

# Welche Arten der Syntaxanalyse gibt es?
=> kam schon. top down, bottom up