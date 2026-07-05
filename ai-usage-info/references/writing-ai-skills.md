# How to write ai skills

# Update AI Usage Info

Diese Skill aktualisiert die projektweite Datei `.ai-usage-info.md`, damit andere KI-Agenten schnell verstehen, wofür die Library gedacht ist und wie sie verwendet wird.
Andere Agenten scannen das ./vendor/* und ./node_modules/* Verzeichnis nach Libraries und lesen die Datei `.ai-usage-info.md` ein, um zu verstehen, mit welchen Libraries
sie arbeiten sollen.

Die .ai-usage-info.md Datei sollte daher möglichst kurz und prägnant sein, damit die KI-Agenten schnell die relevanten Informationen erfassen können.

## Dokumentation mit Beispielen

Längere Codeabschnitte sollten direkt im Verzeichnis `./examples/` liegen und in der .ai-usage-info.md Datei nur verlinkt werden. So können die Beispiele direkt im Code getestet werden.

Erstelle nur Beispiele und Dokumentation für Funktionen und Klassen, die vom Benutzer direkt genutzt werden sollen.
Dokumentiere eine internen funktionen oder Klassen (außer diese sind für den nutzer Relevant).


## Vorgehen

1. Projektkontext erfassen:
    - `composer.json` lesen, insbesondere `name`, `description`, `autoload.psr-4`, `autoload.files`, `require` und `suggest`.
    - Ignoriere erstmal die Readme-Datei, da diese oft zu lang ist und nicht die relevanten Informationen für KI-Agenten enthält.
    - Quellcode unter `src/` prüfen, insbesondere öffentliche Klassen, Interfaces, Traits und globale Funktionen.
    - Beispiele unter `examples/` sowie Tests unter `tests/` prüfen, falls vorhanden.

2. `.ai-usage-info.md` aktualisieren:
    - Platzhalter wie `<!-- Anweisungen -->>` ersetzen.
    - Bestehende sinnvolle Inhalte erhalten und nur veraltete oder falsche Angaben ändern.
    - Keine Funktionen, Beispiele oder APIs erfinden.
    - Links nur setzen, wenn die Zieldateien tatsächlich existieren.

3. Inhaltliche Struktur beibehalten oder sinnvoll ergänzen:
   Orientiere dich bei der Struktur am [Beispiel PHP Library](.ai-usage-info.demo-php.md).

4. Qualität prüfen:
    - Relative Links verifizieren.
    - PHP-Namespace und Funktionsnamen exakt aus dem Code übernehmen.
    - Bei fehlenden Informationen ausdrücklich knapp dokumentieren, dass keine Beispiele/Funktionen gefunden wurden.

## Schreibstil

- Sprache: Deutsch.
- Kurz, sachlich und agentenfreundlich.
- Markdown verwenden.
- Fokus auf konkrete Nutzungshinweise und Beispiele statt Marketingtext.

## Beispiele

Beispiele sollten:

- Sich nicht wiederholen. Erweitere ggf ähnliche Beispiele anstatt zu viele Beispiele zu erstellen. Dokumentiere
  die Beispiele mit Kommentaren im Code.
- Verlinke alle Beispiele in der `.ai-usage-info.md` Datei, damit andere Agenten diese direkt im Code testen können.
- Frage nach, bevor Du ein neues Beispiel anlegst.

## Inline Beispiele

Wenn du einzelne Funktionen dokumentierst, schreibe kurze assert() Beispiele direkt in die `.ai-usage-info.md` Datei, damit andere Agenten diese direkt testen können.

Beispiel PHP:
```php
// meine_methode: kurze Beschreibung, was die Funktion macht
assert(meine_methode($param1, param2) === 'Erwartetes Ergebnis'); // Kurze Beschreibung, was die Funktion macht
assert(meine_methode($param1, param2) === 'Erwartetes Ergebnis'); // Kurze Beschreibung, was die Funktion macht

// meine_methode2: kurze Beschreibung, was die Funktion macht
assert(meine_methode2($param1, param2) === 'Erwartetes Ergebnis'); // Kurze Beschreibung, was die Funktion macht
...
```

Beispiel SCSS (Variablen):

```scss
--variable: #000; // Kurze Beschreibung, was die Variable macht
--variable2: #fff; // Kurze Beschreibung, was die Variable macht
```


## Beispiele für Sprachen:

- [Beispiel PHP Library](.ai-usage-info.demo-php.md).
- [Beispiel SCSS Theme](.ai-usage-info.demo-scss.md).
