# Concept: Paid Workshops

Architektur-Konzept und Fallbeispiel für bezahlte Workshops auf Open Learn.

## Womit anfangen

1. **Erst lesen:** [`WEM-GEHOERT-WAS.md`](WEM-GEHOERT-WAS.md) — klärt die wichtigste Frage: welcher Teil gehört dem Anbieter, welcher Open Learn.
2. **Dann durchklicken:** [`fallbeispiel/README.md`](fallbeispiel/README.md) — der komplette Durchlauf von der Verkaufs-Seite bis zum freigeschalteten Kurs.
3. **Dann das Konzept:** [`specs/001-paid-workshops.md`](specs/001-paid-workshops.md) — der Text für die Diskussion mit Felix.

## Ordner

| Ordner | Zweck |
|---|---|
| `WEM-GEHOERT-WAS.md` | Die Eigentums-Frage geklärt — Anbieter vs. Open Learn |
| `specs/` | Das Konzept zur Diskussion |
| `plans/` | Wie das Fallbeispiel aufgebaut ist |
| `fallbeispiel/` | Das durchklickbare Mockup |
| `fallbeispiel/1-ANBIETER/` | Alles, was dem Kurs-Anbieter gehört |
| `fallbeispiel/2-OPENLEARN/` | Alles, was der Plattform Open Learn gehört |
| `fallbeispiel/diagramme/` | Architektur- und Ablauf-Diagramme |
| `analysis/` | Auswertung nach jeder Felix-Iteration (kommt später) |

## Das Fallbeispiel ansehen

Live im Browser öffnen — kein Setup, kein Server nötig:

```
https://openlearnapp.github.io/concept-paid-workshops/fallbeispiel/1-ANBIETER/landing-page/
```

Von dort durchklicken: Kostenlos starten → Kaufen → Bezahlen → Freischalt-Mail → Vollzugang.
Die Trailer-Videos sind eingebettet, „Kostenlos starten" führt in die live Open-Learn-App.

## Prinzip in einem Satz

Open Learn bleibt statisch und kostenlos und rendert nur. Verkauf, Bezahlung und Marke
gehören dem Anbieter und passieren auf seiner eigenen Landing-Page. Open Learn bekommt
nur eine YAML-URL und weiß nichts von Geld.

## Status

Konzept v1 · Fallbeispiel als Mockup · keine Implementation · zur Diskussion mit Felix
