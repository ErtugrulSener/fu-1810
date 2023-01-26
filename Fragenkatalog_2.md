# Warum übersetzt man überhaupt? 
=> kam schon

# Prinzipieller Ablauf eines Übersetzers
=> kam schon

# Was passiert global über allen Phasen:
Fehlererkennung und Symbtoltabelle

# Unterschied Compiler - Interpreter 
=> kam schon

# Lexikalische Analyse 
# reguläre Ausdrücke, formale Sprachen.
Ein regulärer Ausdruck ist eine Zeichenfolge, mit der man andere Zeichenfolgen erkennen kann.  

# Was ist eine Sprache? (nicht unbedingt eine formale Sprache, ganz allgemein). 
???

# DEA erklären:
erkennt reguläre Ausdrücke Implementierung DEA per Hand: 
Zustandsdiagramme implementieren (nur kurs angedeutet)
Implementierung DEA per Lex: Lex überführt die Spezifikation in C-Quellcode. Die Lex-Spezifikation enthält C-Code (z.B. return TOKEN). Token werden an den Parser weitergereicht. 
Mein Beispiel (nicht wirklich Lex): RegExp: NUMBER [0-9]* -> return NUMBER -> Rückfrage: Und wie kommt die Zahl selbst in den Scanner: yylval

# Syntaxanalyse 
beide Verfahren kurz erläutert
konkreter: Buttom-Up. Analyse: allg. Ablauf, Stack, 4 Befehle 
Was ist das einfachste Verfahren? Operator-Vorrang-Analyse, erläutert: Operatoren, Operator-Tabelle, Erkennen von Handles
=> kam schon

# Attributierte Grammatiken
Erweitern die kontextfreie Grammatik um Attritbute. Semantik kann kontextsensitiv überprüft werden. z.B. Typecheck, Deklaration von Variablen vor der verwendung...

# synthetisierte & vererbte Attribute erklären und unterscheiden
Attribute können entweder synthetisiert, oder vererbt auftreten.
- Synthetisiert: Das Attribut wird aus den Attributen der Kinderknoten berechnet. => Semantische Werte werden einfach hochgereicht.
- Vererbt: Das Attribut wird von Eltern oder Geschwisterknoten berechnet. => Der Wert wird von einem Teilbaum in den anderen Teilbaum hineingegeben.

# S-attributierte Definition & L-attributierte Definition erklären & unterscheiden 
S-Attributiert: Alle Attribute werden synthetisiert. Bsp:
```
E -> AB {E.val := A.val + B.val}
```
L-Attributiert: Man darf nur von linken Geschwisterknoten erben, oder vom Elternknoten. Das L steht für "von links nach rechts". Bsp: 
```
E -> AB {B.val := A.val}

oder:

E -> AB {A.val := E.val
		B.val := A.val}
```