# Regex in PHP: Der Komplette Guide vom Anfänger zum Profi

Reguläre Ausdrücke (Regex) sind ein mächtiges Werkzeug, um Text zu durchsuchen, zu validieren und zu manipulieren. Obwohl sie auf den ersten Blick komplex erscheinen mögen, sind sie ein unverzichtbares Werkzeug für jeden PHP-Entwickler. In diesem Artikel zeige ich dir, wie du Regex in PHP effektiv nutzen kannst – von den Grundlagen bis zu fortgeschrittenen Techniken.

---

## 1. Was ist Regex?

Reguläre Ausdrücke (Regex) sind eine spezielle Syntax, um Muster in Texten zu beschreiben. Sie werden in vielen Programmiersprachen, Texteditoren und Tools verwendet, um Texte zu durchsuchen, zu validieren oder zu transformieren.

### Wofür wird Regex verwendet?
- **Textsuche**: Finde bestimmte Muster in einem Text (z. B. alle E-Mail-Adressen in einem Dokument).
- **Textvalidierung**: Überprüfe, ob ein Text einem bestimmten Muster entspricht (z. B. eine gültige Telefonnummer).
- **Textersetzung**: Ersetze Teile eines Texts basierend auf einem Muster (z. B. alle URLs durch Hyperlinks ersetzen).
- **Datenextraktion**: Extrahiere spezifische Informationen aus einem Text (z. B. alle Hashtags aus einem Social-Media-Post).

### Warum ist Regex wichtig?
Regex ist ein universelles Werkzeug, das in vielen Bereichen der Softwareentwicklung eingesetzt wird. Es ist besonders nützlich, wenn du mit Texten arbeitest, die komplexe Muster enthalten. Obwohl Regex auf den ersten Blick kompliziert erscheinen mag, lohnt es sich, die Grundlagen zu lernen, da es dir viel Zeit und Aufwand sparen kann.

### Beispiel: Einfache Regex in PHP
```php
// Überprüfen, ob ein String nur Buchstaben enthält
if (preg_match("/^[a-zA-Z]+$/", "HelloWorld")) {
    echo "Valid!";
} else {
    echo "Invalid!";
}
```

## 2. Grundlagen der Regex

### Zeichenklassen
Zeichenklassen definieren eine Gruppe von Zeichen, die an einer bestimmten Stelle im Text vorkommen können.

- `[a-z]`: Kleinbuchstaben von a bis z
- `\d`: Eine Ziffer (0–9)
- `\w`: Ein Wortzeichen (Buchstaben, Ziffern oder Unterstrich)

### Beispiel:  
```php
// Überprüfen, ob ein String nur Buchstaben enthält
if (preg_match("/^[a-zA-Z]+$/", "HelloWorld")) {
    echo "Valid!";
}
```

### Quantoren
Quantoren legen fest, wie oft ein Zeichen oder eine Zeichenklasse vorkommen darf.

- `*`: Null oder mehr
- `+`: Ein oder mehr
- `?`: Null oder eins
- `{n,m}`: Zwischen n und m Mal

### Beispiel:  
```php
// Überprüfen, ob ein String zwischen 3 und 5 Ziffern enthält
if (preg_match("/^\d{3,5}$/", "1234")) {
    echo "Valid!";
}
```

### Gruppierung
Gruppierung ermöglicht es, Teile eines Musters zu kombinieren.

- `(abc)`: Gruppiert die Zeichen „abc
- `a|b`: Entweder „a“ oder „b“

### Beispiel:  
```php
// Überprüfen, ob ein String „cat“ oder „dog“ enthält
if (preg_match("/(cat|dog)/", "I love cats!")) {
    echo "Match found!";
}
```

## 3. Fortgeschrittene Techniken

### Lookaheads
Lookaheads ermöglichen es, nach Mustern zu suchen, ohne sie in das Ergebnis aufzunehmen.

- `(?=...)`: Positiver Lookahead
- `(?!...)`: Negativer Lookahead

### Beispiel:  
```php
// Passwortvalidierung: Mindestens 8 Zeichen, 1 Großbuchstabe, 1 Zahl
if (preg_match("/^(?=.*[A-Z])(?=.*\d).{8,}$/", "Secure123")) {
    echo "Strong password!";
}
```

### Benannte Gruppen
Benannte Gruppen ermöglichen es, Teile eines Musters zu benennen und später zu referenzieren.

x `(?<name>...)`: Benennt eine Gruppe

### Beispiel:  
```php
// Datum im Format JJJJ-MM-TT extrahieren
if (preg_match("/(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/", "2025-01-05", $matches)) {
    echo "Year: " . $matches['year']; // Output: 2025
}
```

### Greedy vs. Lazy Quantoren
- Greedy: Der Quantor versucht, so viel Text wie möglich zu matchen
- Lazy: Der Quantor versucht, so wenig Text wie möglich zu matchen

### Beispiel:  
```php
// Greedy vs. Lazy
$text = "abcabcabc";
preg_match("/a.*c/", $text, $greedy); // Matches "abcabcabc"
preg_match("/a.*?c/", $text, $lazy);  // Matches "abc"
```

## 4. Praktische Anwendungen

### Textersetzung
Mit `preg_replace` kannst du Text ersetzen

### Beispiel:  
```php
// Alle Vokale durch „*“ ersetzen
$text = "Hello World!";
$result = preg_replace("/[aeiou]/i", "*", $text);
echo $result; // Output: H*ll* W*rld!
```

### Daten extrahieren
Du kannst spezifische Daten aus einem Text extrahieren.

### Beispiel:  
```php
// URLs aus einem Text extrahieren
$text = "Visit https://example.com or http://test.org for more info.";
preg_match_all("/https?:\/\/[^\s]+/", $text, $matches);
print_r($matches[0]); // Output: Array mit URLs
```

### Validierung
Regex eignet sich hervorragend zur Validierung von Benutzereingaben.

### Beispiel:  
```php
// E-Mail-Validierung
$email = "test@example.com";
if (preg_match("/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/", $email)) {
    echo "Valid email!";
}
```

## 5. Performance-Tipps

Regex ist zwar mächtig, kann aber bei falscher Anwendung Performance-Probleme verursachen. Hier sind einige Tipps, um sicherzustellen, dass deine Regex effizient und performant sind:

### 1. Vermeide komplexe Regex
- Problem: Sehr komplexe Regex-Muster können langsam sein, insbesondere bei großen Texten
- Lösung: Zerlege komplexe Muster in einfachere Teile oder verwende alternative Methoden (z. B. String-Funktionen wie `strpos` oder `str_replace`)

### Beispiel:  
Statt:
```php
preg_match("/^(a|b|c|d|e|f|g|h|i|j|k|l|m|n|o|p|q|r|s|t|u|v|w|x|y|z)+$/", $text);
```
Besser:
```php
preg_match("/^[a-z]+$/i", $text);
```

### 2. Nutze `preg_match_all` sparsam
- Problem: `preg_match_all` durchsucht den gesamten Text und kann bei großen Texten langsam sein
- Lösung: Verwende `preg_match`, wenn du nur das erste Vorkommen eines Musters suchst.

### Beispiel:  
Statt:
```php
preg_match_all("/\d+/", $text, $matches);
```
Besser (wenn nur das erste Vorkommen benötigt wird):
```php
preg_match("/\d+/", $text, $matches);
```

### 3. Cache-Ergebnisse
•	Problem: Wenn du dieselbe Regex-Operation mehrmals ausführst, kann das die Performance beeinträchtigen.
•	Lösung: Speichere die Ergebnisse von Regex-Operationen in Variablen oder einer Datenbank, um sie später wiederzuverwenden.

### Beispiel:  
```php
$pattern = "/^[a-z]+$/i";
$result = preg_match($pattern, $text);
if ($result) {
    // Ergebnis verwenden
}
```

### 4. Nutze `preg_quote` für dynamische Muster
Problem: Wenn du Benutzereingaben in Regex einbindest, können Sonderzeichen zu Fehlern führen.
Lösung: Verwende `preg_quote`, um Sonderzeichen zu escapen.

### Beispiel:  
```php
$userInput = "test.com";
$pattern = "/^" . preg_quote($userInput, "/") . "$/";
if (preg_match($pattern, "test.com")) {
    echo "Match!";
}
```

## 6. Zusammenfassung und Ressourcen

### Zusammenfassung
Regex ist ein unverzichtbares Werkzeug für die Textmanipulation in PHP. Mit den Grundlagen und fortgeschrittenen Techniken, die du in diesem Artikel gelernt hast, kannst du:
- Texte durchsuchen und validieren
- Komplexe Textmuster erkennen und extrahieren
- Texte effizient ersetzen und transformieren

Wichtige Punkte zum Mitnehmen
1.	Grundlagen: Lerne die Grundlagen wie Zeichenklassen, Quantoren und Gruppierung
2.	Fortgeschrittene Techniken: Nutze Lookaheads, benannte Gruppen und Greedy/Lazy Quantoren für komplexe Muster
3.	Performance: Achte auf die Performance deiner Regex und vermeide unnötige Komplexität

Weiterführende Ressourcen
- [Regex101](https://regex101.com/): Ein interaktives Tool zum Testen und Debuggen von Regex.
- [PHP-Dokumentation zu PCRE](https://www.php.net/manual/en/book.pcre.php): Die offizielle Dokumentation zu Regex in PHP.
- [RegexCheatSheet](https://www.rexegg.com/regex-quickstart.html): Eine nützliche Cheat-Sheet für Regex

