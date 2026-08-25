# Vibe-Coded-Math-Stuff — Projekt- und Style-Notizen

Sammlung eigenständiger Mathe-Übungsseiten für eine Grundschulklasse.

## Einsatzsituation (bestimmt fast alle Design-Entscheidungen)

Die Seiten werden **per Beamer an die Tafel projiziert**. Die Kinder sitzen im
U-förmigen Sitzkreis darum herum. Ablauf:

1. Die Seite zeigt eine zufällige Aufgabe.
2. Ein Kind wird drangenommen und **sagt** das Ergebnis laut.
3. Die Lehrkraft drückt **Pfeil nach rechts** — die richtige Lösung erscheint.
   Das genannte Ergebnis wird **nie eingetippt**; alle vergleichen selbst.
4. Nochmal **Pfeil nach rechts** → nächste zufällige Aufgabe.

Daraus folgt:

- **Nur Tastatursteuerung, keine Maus.** Die Lehrkraft steht an der Tafel.
- **Keine Eingabefelder** für Antworten. Nie nach dem Ergebnis fragen.
- **Alles groß und kontrastreich.** Aus der letzten Reihe lesbar, Beamer-Farben
  sind flau. Dünnes Hellgrau nur für Nebensächliches (Fußzeile), nie für Inhalte.
- **Offline lauffähig.** Keine CDNs, keine externen Schriften, keine Abhängigkeiten.

## Technischer Rahmen

- Ein Unterordner je Thema, darin eine einzige, komplett eigenständige
  `index.html` (HTML + CSS + JS in einer Datei). Kein Build, kein npm.
- Sprache der Oberfläche: **Deutsch**.
- Zufällige Aufgaben werden im Browser erzeugt; kein Speichern, kein Server.

## Tastenbelegung (durchgängig gleich halten)

| Taste | Bedeutung |
|---|---|
| `→` | Lösung zeigen, beim zweiten Druck nächste Aufgabe |
| `↑` | Schwierigkeitsgrad oder Variante umschalten (rotierend) |
| `↓` | zusätzliche Darstellungshilfe aus-/einblenden |

`→` ist auf **allen** Seiten belegt und darf seine Bedeutung nie ändern.
`↑`/`↓` sind optional, je nach Thema.

**Schwierigkeitsmodi gelten auch beim Auflösen.** Was der Modus ausblendet,
bleibt beim Anzeigen der Lösung ausgeblendet — sonst springt das Tafelbild und
verwirrt die Kinder. (Ausdrücklicher Wunsch nach Praxistest im Unterricht.)

## Aussehen

### Aufgabenkasten

Weiße Karte auf hellem Hintergrund, mittig im Bild:

```css
background: #ffffff;
border-radius: 30px;                        /* 28–30px */
box-shadow: 0 10px 30px rgba(0,0,0,0.1);    /* der "Drop-Shadow" */
border: 1px solid rgba(0,0,0,0.05);
padding: 40px 50px;                          /* oben mehr, wenn Pille drüber */
```

Body: `--bg: #f8f9fa`, Flex-zentriert, `height: 100vh`, `overflow: hidden`,
`user-select: none`, Schrift `'Segoe UI', Roboto, Helvetica, Arial, sans-serif`.

### Überschrift als Pille — **gewünschter Standard**

Blaue Pille mit dem Namen des Aufgabentyps, die **mittig auf der oberen
Kartenkante sitzt: etwa 30 % ragen heraus, 70 % liegen in der Karte.**
Viele Kinder vergessen die Fachbegriffe („Zahlenstrahl", „Verliebte Zahlen"),
deshalb steht der Name immer sichtbar an derselben Stelle.

> **Wichtig:** Die meisten älteren Seiten haben diese Pille noch **nicht** oder
> haben sie vollständig innerhalb der Karte. Das ist **kein Gegenbeispiel**,
> sondern Nachrüstbedarf. Bei neuen Seiten immer die herausragende Variante
> verwenden. Referenz-Umsetzung: `Zahlenstrahl-ZR100/index.html`.

```css
.main-card { position: relative; padding-top: 58px; }

.title-pill {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translate(-50%, -30%);
    background: var(--blue);
    color: #ffffff;
    font-size: 22px;
    font-weight: 500;
    padding: 10px 32px;
    border-radius: 999px;
    width: fit-content;
    white-space: nowrap;
    letter-spacing: 0.3px;
    box-shadow: 0 4px 12px -2px rgba(33,150,243,0.4);
}
```

**Falle, die schon einmal zugeschlagen hat:** Die beiden Prozentwerte in
`translate()` sind unabhängig und beziehen sich beide auf die **Pille selbst** —
der erste auf ihre Breite, der zweite auf ihre Höhe. Für die Aufteilung
außen/innen ist **nur der zweite** zuständig. Der erste muss `-50%` bleiben, denn
der zentriert waagerecht. Wer ihn ändert und dann mit `left` gegensteuert, baut
einen breitenabhängigen Fehler ein: `left` rechnet in Prozent der **Karte**,
`translate` in Prozent der **Pille** — der Ausgleich stimmt dann nur bei genau
einer Fensterbreite und verrutscht am Beamer wieder.

### Anleitungsnotiz unten

Dezente Fußzeile mit der Tastenbelegung, damit die Lehrkraft die Sondertasten
nicht auswendig können muss. Zwei etablierte Varianten — beide sind okay:

```css
/* schlicht, unterhalb der Karte */
.hint { margin-top: 24px; color: #999; font-size: 16px; text-align: center; }

/* als Pille am unteren Bildrand */
.footer-hint {
    position: absolute; bottom: 30px; font-size: 16px; color: #aaa;
    background: rgba(0,0,0,0.03); padding: 8px 20px; border-radius: 20px;
}
```

Text nennt die Tasten als Pfeilzeichen, z. B.:
`Tipp: → zeigt die Lösung, noch einmal → bringt die nächste Aufgabe.`
Zeigt eine Seite einen umschaltbaren Modus, gehört der **aktuelle Modusname**
mit in die Fußzeile.

### Farben

```css
--blue: #2196F3;      /* Standardblau: Lösungen, Überschrift-Pille */
--bg: #f8f9fa;
--card-bg: #ffffff;
```

Aufgedeckte Lösungen erscheinen **blau und fett** — deutlich abgesetzt von der
schwarzen Aufgabenstellung. Zahlen und Beschriftungen fast reines Schwarz
(`#0d0d0d`–`#333`), Linien/Hilfsgeometrie dunkles Grau (`#3a3a3a`).
`Zehneruebergang` und `Verdoppeln-Halbieren` nutzen ein weicheres Blau
(`#4f8edc` / `#4a9fd4`) mit Rot als Gegenfarbe — das ist gewachsen und darf so
bleiben; für Neues das Standardblau nehmen.

### Animationen

Zustandswechsel dürfen animiert werden, wenn sie das Verstehen unterstützen.
Hausmaß: **~320 ms** Dauer mit leichter Überschwing-Kurve
(`cubic-bezier(0.34, 1.5, 0.64, 1)`) und, bei vielen gleichartigen Elementen,
**~5 ms Versatz pro Element** von links nach rechts, sodass eine Welle entsteht.
Wichtig: Beim Umschalten die vorhandenen Elemente per CSS-Klasse umschalten
statt neu zu zeichnen — sonst läuft keine Transition.

## Bestehende Seiten

| Ordner | Thema |
|---|---|
| `Zahlenstrahl-ZR100` | Zahl am Zahlenstrahl verorten (ZR 100) |
| `Dienes-ZR100` | Dienes-Material, Zehner/Einer |
| `Zahlzerlegung-ZR20-OZ` | Zahlzerlegung ZR 10/20 ohne Zehnerübergang |
| `Zehneruebergang` | Zehnerübergang in zwei Schritten (Addition über die 10) |
| `Verliebte-Zahlen` | Zahlenzerlegung bis 10 |
| `Verdoppeln-Halbieren` | Verdoppeln und Halbieren |
