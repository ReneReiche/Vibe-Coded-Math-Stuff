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
| `Leertaste` | wirkt genau wie `→` |
| `↑` | Schwierigkeitsgrad oder Variante umschalten (rotierend) |
| `↓` | zusätzliche Darstellungshilfe aus-/einblenden |
| `←` | weitere Variante umschalten (rotierend) |
| Buchstabe | seltener gebrauchter Modus, z. B. `S` für schrittweises Aufdecken |

`→` ist auf **allen** Seiten belegt und darf seine Bedeutung nie ändern.
`↑`/`↓`/`←` sind optional, je nach Thema.

**Die Leertaste nie als Umschalter benutzen.** Sie ist der reflexhafte
Weiter-Knopf und der Vorwärtsknopf vieler Präsentationsfernbedienungen — als
Modusschalter würde sie mitten in der Stunde unbemerkt etwas verstellen.
Deshalb ist sie ein Zweitname für `→`.

**Sind alle vier Pfeile vergeben, kommen Buchstaben dran, keine Sondertasten.**
Manche Kolleginnen und Kollegen benutzen iPad-Hüllentastaturen, auf denen
gerade die Sondertasten an ungewohnten Stellen sitzen; Buchstaben liegen auf
jeder Tastatur gleich und sind als Anfangsbuchstabe des Modus zusätzlich
merkbar. Der Buchstabe gehört mit in die Fußzeile.

**Schwierigkeitsmodi gelten auch beim Auflösen.** Was der Modus ausblendet,
bleibt beim Anzeigen der Lösung ausgeblendet — sonst springt das Tafelbild und
verwirrt die Kinder. (Ausdrücklicher Wunsch nach Praxistest im Unterricht.)

## Seiten zum Selbstrechnen — Ausnahme von der Sitzkreis-Regel

Zwei Seiten sind **nicht** fürs Tafelbild, sondern für ein Kind am eigenen
Gerät gedacht: `Zehneruebergang` (ZR 20) und `Zehneruebergang-ZR100`.
Dort gelten die Regeln oben teilweise nicht — das ist Absicht und kein
Nachrüstbedarf:

- Sie **haben Eingabefelder** und fragen nach dem Ergebnis.
- `→` bedeutet dort **nicht** „Lösung zeigen“, sondern schaltet zum nächsten
  Eingabefeld; `Enter` bestätigt. Alle vier Pfeile gehören der Eingabe.
- Schriftgrößen dürfen kleiner sein: gelesen wird aus 40 cm, nicht aus der
  letzten Reihe.
- Sie führen Streak und Schwierigkeitsstufe mit, **ohne zu speichern**. Ein
  Neuladen setzt beides zurück; das ist gewollt, damit niemand über Tage
  hinweg sammelt.

**Die Eingabe läuft immer über einen einzigen Controller** (`INPUT.digit`,
`.back`, `.step`, `.bump`, `.submit` in `Zehneruebergang-ZR100`), nicht verteilt
im Tastatur-Listener. Die Kinder arbeiten an iPads mit Hüllentastatur; sollte
später ein antippbares Ziffernfeld dazukommen, ruft es dieselben Funktionen auf
und sonst ändert sich nichts.

**Fehler werden vorgemacht, nicht nur markiert.** Die falsche Zerlegung des
Kindes wird genau so ins Hunderterfeld gelegt, wie es sie eingegeben hat — mit
sichtbarem Vorrat daneben, aus dem die Einer verschwinden. Wer statt 4 + 1 die
Zerlegung 4 + 2 einträgt, sieht den Vorrat leer werden und den sechsten Würfel
rot gestrichelt danebenliegen. Dazu höchstens **ein** Hinweissatz, nicht fünf.

**Der erste Schritt bleibt in seiner Zeile und läuft notfalls heraus.** Das ist
die wichtigste Abweichung von der Regel „zeilenweise von links oben“ weiter
unten, und sie gilt nur hier: Schritt 1 legt weiter in der Zeile, in der die
Einer der Startzahl liegen, Schritt 2 fängt immer am Anfang der nächsten Zeile
an. Bei 85 + 7 mit der Zerlegung 6 und 1 liegen also fünf Einer im neunten
Zehner, sechs kommen dazu — und der sechste ragt rechts aus dem Feld heraus,
in ein gestricheltes Kaestchen. Legt ein Kind zu wenig, bleibt in der Zeile
darüber eine Lücke. Würde stattdessen einfach umgebrochen, wäre der Fehler
unsichtbar: das Material läge genauso wie bei der richtigen Zerlegung. Rechts
vom Feld sind dafür vier Spalten reserviert (`RESERVE`); braucht es mehr,
wächst nur der `viewBox` und das Bild rückt zusammen, damit die Seite nicht
springt. Genauso macht es die ZR-20-Seite mit ihrem Zwanzigerfeld.

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

### Credit-Zeile mit Claw'd — **Standard für jede Seite**

Unter der Fußzeile steht eine noch kleinere, noch blassere Zeile, die die
Beteiligten nennt, gefolgt vom Claw'd-Maskottchen als Pixelfigur:

```
Idee und Didaktik: René Reiche · Code: Claude (AI)  [Claw'd]
```

Wortlaut ist abgestimmt und bleibt so: „AI", nicht „KI"; „Claude", nicht
„Claw'd" im Text; kein „Anthropic". Das Maskottchen ist ein Inline-SVG auf
einem 12 × 9-Raster (Körper, zwei Scheren, vier Beine, zwei Augen), Farbe
`#d97757`, Augen `#1a1a1a`, **36 × 27 px** — genau 3 px je Rasterfeld, damit
es bei 100 % Zoom pixelscharf ist. **Kein** `shape-rendering="crispEdges"`:
das rundet bei krummen Zoomstufen ein Auge auf 2 und das andere auf 3 px;
mit Kantenglättung bleiben beide gleich breit.

```css
.credit { margin-top: 8px; font-size: 11px; color: #bbb; text-align: center;
          display: flex; align-items: center; gap: 6px; }
.credit .mascot { width: 36px; height: 27px; opacity: 0.85; }
```

Markup und SVG zum Kopieren: `Ergaenzen-Hunderterfeld-ZR100/index.html`
(erste Seite mit dieser Zeile). Ältere Seiten haben sie noch nicht —
Nachrüstbedarf, kein Gegenbeispiel.

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

### Dienes-Material

Einer liegen **rechts neben den Zehnerstangen**, auf Höhe der untersten Stange,
so wie im *Denken & Rechnen*-Heft. Fünferlücke nach der fünften Stange.

> **Nachrüstbedarf:** `Dienes-Addition-ZR100` legt die Einer noch in eine Zeile
> **unter** den Stangenblock. Neue Seiten machen es wie
> `Dienes-Subtraktion-ZR100`.

Wegnehmen wird **durchgestrichen, nicht mit einer Hand angedeutet**. Ein
dunkelroter Strich (`#c62828`) pro Materialgruppe, gezogen über die Diagonale
des weggenommenen Blocks von oben links nach unten rechts, runde Enden, an
beiden Enden 0,25 u über die Holzkante hinaus. Bei einer einzelnen Stange ergibt
diese Regel automatisch einen fast waagerechten Strich, bei sieben einen
steilen — ein Sonderfall weniger. Danach sinkt das durchgestrichene Material auf
45 % Deckkraft: durchgestrichen heißt zurückgetreten, nicht unsichtbar, denn
gezählt werden muss es noch.

Gründe gegen die ausgeschnittene Hand aus dem Heft: sie greift dort drei bis
vier Stangen und lässt sich nicht auf sieben strecken, für Einerwürfel gibt es
gar keine passende Haltung, ein Raster-PNG ist am Beamer flau, und die Seiten
sollen assetfrei bleiben.

**Zwei getrennt liegende Materialgruppen bedeuten immer Addition.** Deshalb
wird beim Minus nichts zur Seite geschoben, solange die Aufgabe noch offen ist —
sonst zeigt das Bild zu `34 − 20` genau das Bild zu `14 + 20`. Erst beim
Auflösen darf das Weggestrichene wegrutschen; was übrig bleibt, bewegt sich
dabei nicht, denn der Rest **ist** die Lösung.

### Hunderterfeld

Zehn mal zehn Kästchen mit dünnen grauen Linien; nach der fünften Spalte und
der fünften Zeile eine dicke Linie, die wie im *Denken & Rechnen*-Heft ein
Stück über den Rand hinausragt (Kraft der Fünf). Gefüllt wird **zeilenweise
von links oben.**

> Ausnahme: Auf den Seiten zum Selbstrechnen legt das Kind schrittweise, und
> dann bleibt ein Schritt in seiner Zeile, statt umzubrechen — siehe oben.

Im Feld liegt **Dienes-Material, keine Wendeplättchen**: Jede volle Zeile ist
**eine Zehnerstange** (ein Stück mit schwacher Kästchenteilung), nur der
Rest sind einzelne **Einerwürfel** mit dunkler Kante. Ein Würfel pro Kästchen
über das ganze Feld wurde ausdrücklich abgelehnt.

Die Startmenge steht **sofort**, ohne Animation. Nur das Ergänzte wird
animiert, und zwar in der Reihenfolge, in der die Kinder rechnen: **erst
Einer bis zum vollen Zehner, dann ganze Zehnerstangen, zuletzt die
restlichen Einer** (46 + _ = 83: vier Würfel, drei Stangen, drei Würfel).
Ergänztes Material ist blau wie die aufgedeckte Zahl. Referenz:
`Ergaenzen-Hunderterfeld-ZR100/index.html`.

### Aufgabenverteilung

Zufällige Aufgaben werden **nicht gleichverteilt über alle Aufgaben** gezogen,
sondern über einen Beutel ohne Zurücklegen. Wonach der Beutel sortiert ist,
hängt von der Rechenart ab — und das ist keine Kleinigkeit:

- **Plus** zieht das **Ergebnis** gleichverteilt und dann eine seiner
  Zerlegungen. Sonst bekommen Ergebnisse mit vielen Zerlegungen zu viel
  Gewicht (100 hat neun, 20 hat eine).
- **Minus** zieht den **Minuenden**. Denselben Trick wie bei Plus zu nehmen
  wäre falsch herum: beim Minus ist der Minuend die größte Zahl der Aufgabe,
  ein gleichverteiltes Ergebnis erzwingt also einen großen Minuenden. Gemessen
  lag der Minuend dadurch im Mittel bei **80** (Z − Z) und **77,5** (ZE − ZE) —
  fast nur Aufgaben aus dem oberen Drittel.

**Merksatz: gleichverteilt gehört die Zahl, die in der Aufgabe die größte sein
kann — nicht die, die das Kind sagt.**

Zusätzlich liegen kleine Minuenden mehrfach im Beutel, sonst bleibt der
Mittelwert am Mittelpunkt des Zahlenbereichs hängen. Dabei braucht es eine
Deckelung: ein Minuend mit nur einer möglichen Zerlegung würde seine eine
Aufgabe sonst ständig wiederholen (`20 − 10` in jeder sechsten Aufgabe).
Umsetzung mit den drei abgewogenen Konstanten in
`Dienes-Subtraktion-ZR100/index.html`.

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
| `Dienes-Addition-ZR100` | Plus mit Dienes-Material: Z + Z und Z + ZE (ZR 100) |
| `Dienes-Subtraktion-ZR100` | Minus mit Dienes-Material: Z − Z, ZE − E, ZE − ZE (ZR 100) |
| `Ergaenzen-Hunderterfeld-ZR100` | Ergänzen auf dem Hunderterfeld, vier Stufen per `↓` (nächster Zehner, im selben Zehner, höherer Zehner, beliebige Zahl); `↑` nur symbolisch |
| `Zahlzerlegung-ZR20-OZ` | Zahlzerlegung ZR 10/20 ohne Zehnerübergang |
| `Zehneruebergang` | Zehnerübergang in zwei Schritten (Addition über die 10) |
| `Zehneruebergang-ZR100` | Zehnerübergang in zwei Schritten bis 100, **von Kindern selbst bearbeitet**: Zerlegung eintippen, danach Kontrolle am Hunderterfeld |
| `Verliebte-Zahlen` | Zahlenzerlegung bis 10 |
| `Verdoppeln-Halbieren` | Verdoppeln und Halbieren |
