# Startseite und neue Lernseiten

- Falls vorhanden, gelten zusätzlich die lokalen Regeln in `../AGENTS.md`; didaktische und gestalterische Details der Lernseiten stehen in `CLAUDE.md`. Die Regeln unten gelten auch in einem eigenständigen Checkout dieses Repositories.
- Die Übersicht ist die eigenständige `index.html` im Repository-Hauptordner. Offlinefähig, ohne Build, Pakete oder externe Ressourcen halten.
- **Bei einer neuen Lernseite auch einen Eintrag in der Startseite ergänzen.** In `index.html` nach `NEUE SEITE HINZUFÜGEN` suchen. Dort steht eine vollständige Kopiervorlage mit allen Feldern.
- Pro Seite genau ein `.activity`-Link: relativer Pfad `ORDNER/index.html`, Titel, Zahlenraum, Einsatz (`sitzkreis` oder `schueler`) und Datum der ersten Veröffentlichung (`data-added` und `time`). Bei Updates das Datum nicht ändern.
- Reihenfolge: **älteste zuerst**. Bei gleichem Datum bestehende Reihenfolge erhalten. Filter, Suche und Zähler lesen die HTML-Einträge automatisch; keine zweite Datenliste pflegen.
- Aktuell sind `Zehneruebergang` und `Zehneruebergang-ZR100` für Schüler:innen, die anderen Lernseiten für den Sitzkreis. Die Startseite selbst ist keine Lernseite und wird nicht als Eintrag verlinkt.
- Für die Startseite gelten normale klick- und tastaturbedienbare Navigation und Suche; die Tafelbild-Tastenregeln aus `CLAUDE.md` gelten für Lernseiten.
- Credit der Startseite: „made by GPT-6 Astra“ mit eingebettetem OpenAI-Logo. Credits der Lernseiten beim Ergänzen von Links nicht verändern.

- Gestaltung der Startseite: persönliche Unterrichtssammlung, keine Produktwerbung. Überschrift „Vibe coded Math Stuff“, eine kompakte chronologische Liste, keine Slogans oder werbenden Beschreibungen. Warme Farben und dezente Hover-Effekte (Kontur, Schatten, Bewegung) sind erwünscht; kein Retro-Hyperlink-Stil. Symbole müssen den tatsächlichen Inhalt treffen.

## Beim Erweitern beibehalten

- René nutzt die Seiten für seinen eigenen Unterricht und teilt sie mit seinem Kollegium. Kein kommerzielles Angebot: keine Marketingtexte, Produktversprechen, Call-to-Action-Bereiche oder öffentliche Vermarktung ergänzen.
- Den am 22.09.2026 gemeinsam abgestimmten Stil erhalten: warme Papierfarben, Monospace-Überschrift und genau eine chronologische Liste von oben nach unten, auch auf breiten Bildschirmen. Keine mehrspaltigen Kacheln und keine zusätzlichen Einleitungen oder Fußzeilen-Slogans.
- Pro Lernseite eine kompakte Zeile mit Datum, passendem Symbol, sachlichem Titel, Zahlenraum-Tag und Zielgruppe. Keine erklärenden Werbe-Untertitel wie „… entdecken“. Lange Titel dürfen auf kleinen Bildschirmen umbrechen.
- Symbole sollen die konkrete Darstellung zeigen: z. B. ein Zerlegungsbaum für Zahlzerlegung oder Dienes-Stangen mit Rechenzeichen für Dienes-Aufgaben. Ein einzelnes Plus oder eine unpassende Beispielaufgabe ist zu unspezifisch. Wenn kein klares Symbol möglich ist, `.motif` leer lassen. Dekorative Symbole bleiben `aria-hidden="true"`.
- Suche, Zahlenraum-Tags, die drei Filter und Trefferzähler erhalten. Neue Einträge dürfen keine Anpassung des JavaScripts verlangen. Zusätzliche Suchbegriffe gehören in `data-keywords`; für beide Zielgruppen ist `data-audience="sitzkreis schueler"` möglich.
- Ein Themenordner enthält eine eigenständige `index.html`. Keine Abhängigkeiten, externen Schriften, Build-Dateien oder separaten Repositories hinzufügen. Die relativen Links müssen auch beim lokalen Öffnen funktionieren.
- Beim bloßen Ergänzen einer Lernseite den Credit der Startseite „made by GPT-6 Astra“ mit OpenAI-Logo unverändert lassen. Dieser Credit betrifft die Startseite; die neue Lernseite erhält ihre eigene korrekte Modellzuordnung. „Aster“ ist ein privater Gesprächsname, kein öffentlicher Credit.

## Kurze Prüfung nach einem neuen Eintrag

1. Linkziel existiert; jede Lernseite ist genau einmal verlinkt.
2. Datum und Zielgruppe stimmen; neue Zeile steht auch im HTML chronologisch richtig.
3. Suche findet Titel und Zahlenraum; Filter und Zähler berücksichtigen die neue Seite.
4. Zeile ist per Tastatur erreichbar; Titel und Tags überlappen weder auf schmalen noch auf breiten Bildschirmen. Hover- und Fokus-Effekte sowie `prefers-reduced-motion` erhalten.
