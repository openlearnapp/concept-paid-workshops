# Analysis 001 — Mockup vs. Live-Implementierung

## Stand 2026-05-31

Das Konzept ist nicht mehr nur Idee: die Premium-Workshop-Funktion ist parallel in der echten Open-Learn-App in Umsetzung (siehe `plans/002-integration-in-open-learn.md`). Das Fallbeispiel hat damit zwei Ebenen — Mockup und echte App.

## Was der Mockup zeigt

Statische HTML-Seiten unter `fallbeispiel/2-OPENLEARN/`:

| Seite | Was sie demonstriert |
|---|---|
| `workshops.html` | Workshop-Übersicht mit Premium-Hervorhebung |
| `workshop-preview.html` | Lernpfad vor dem Kauf — Schloss-Symbole bei gesperrten Lektionen |
| `workshop-unlocked.html` | Lernpfad nach dem Kauf — alle Lektionen offen |

**Vorteil Mockup:** sofort durchklickbar, jeder Reviewer sieht den Flow ohne Setup. Kein Branch-Wechsel, keine App-Erweiterung nötig.
**Limit:** statisch, kein echtes Datenmodell, kein Bezug zum Workshop-YAML.

## Was die Live-Implementierung zeigt

In `openlearnapp/openlearnapp.github.io` und im Demo-Workshop `openlearnapp/workshop-linux-grundlagen-preview`:

- YAML-Konfiguration: Anbieter wählt frei welche Lektionen frei sind, welche gesperrt
- Werbe-Banner unter dem Trailer mit Anbieter-Branding (Logo, Headline, Pitch, Preis, CTA)
- Schloss-Karten: gleiche Form wie freie Lektionen, dezentes Schloss-Symbol auf dem Thumbnail
- URL-Guard: direkter Lesson-URL-Aufruf einer gesperrten Lektion leitet zurück auf die Übersicht
- Demo-Unlock per LocalStorage (für Reviewer)

**Vorteil Live:** echtes Datenmodell, das Anbieter sofort selbst verwenden können. **Limit:** abhängig vom App-Deployment und vom Demo-Workshop-Pages-Build.

## Welche Fragen das Live-System bereits beantwortet

| Frage aus dem ursprünglichen Konzept | Antwort jetzt |
|---|---|
| Wie sieht ein gesperrter Lernpfad aus? | Schloss-Karten in Anbieter-Akzentfarbe, identische Form wie freie Karten |
| Wo entscheidet der Anbieter welche Lektionen frei sind? | YAML-Felder `free_lessons` (Anzahl) oder `free_lesson_numbers` (Liste) |
| Wo bewirbt der Anbieter den Kurs? | Banner direkt unter dem Trailer-Video, Branding über `provider:` Block |
| Wo passiert der Kauf? | Externer Link aus `provider.landing_url` — Open Learn bleibt statisch |

## Welche Fragen noch offen sind

- Endgültiger Zugangs-Schutz nach dem Kauf (Path-as-Secret vs. signierte Tokens)
- Wie Lernende einen gekauften Workshop auf neuen Geräten erneut entsperren
- Refund-Mechanik und Umsatzbeteiligung — beides Geschäfts-, nicht Implementierungsfragen
- Discovery: Open-Learn-eigene Premium-Liste oder reine Anbieter-Discovery?
