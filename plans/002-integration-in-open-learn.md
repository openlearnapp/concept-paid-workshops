# Plan 002 — Integration in die echte Open-Learn-App

## Ziel

Das Konzept aus `specs/001-paid-workshops.md` in der produktiven Open-Learn-App umsetzen, sodass Anbieter ihre Workshops als Premium markieren können und Lernende sie kaufen + freischalten können.

## Aufteilung in PRs (1 Sektion = 1 PR)

Die Implementierung läuft im Plattform-Repo `openlearnapp/openlearnapp.github.io` und ist in mehrere PRs aufgeteilt, damit jede Sektion einzeln reviewbar bleibt:

1. **Quiz-Bot entfernen** — Voraussetzung für ruhigen Lese-Flow, unabhängig vom Premium-System (gemerged 2026-05-31)
2. **Premium-Backbone** — Schema in `workshops.yaml` (Felder `premium`, `free_lessons`, `free_lesson_numbers`, `provider`), Werbe-Banner unter dem Trailer, Schloss-Karten für gesperrte Lektionen, URL-Guard im LessonDetail
3. **Premium-Indikator auf Workshop-Karten** — Aurora-Rand + Stern-Badge in der Workshop-Liste, Anbieter-Strip mit Preis
4. **Anbieter-Onboarding auf der Startseite** — Erklär-Sektion „Verkaufe deinen Kurs über Open Learn" mit YAML-Snippet
5. **Creators-Seite Cinematic Redesign** — vollständige Premium-Sektion mit Konfigurations-Beispielen und Live-Demo-Link

## Demo-Workshop

Für jede der PRs ist ein Demo-Workshop live testbar:

- Repo: `openlearnapp/workshop-linux-grundlagen-preview`
- Live: https://open-learn.app/workshop-linux-grundlagen-preview/
- Anbieter (fiktiv): „LINUXPFAD Akademie"
- Konfiguration: 3 freie Lektionen, 10 gesperrte, Verkaufs-URL als Platzhalter

## Übergang vom Mockup zum Live-System

Sobald PR 2 (Premium-Backbone) auf `open-learn.app` deployed ist, werden die Links in `fallbeispiel/1-ANBIETER/landing-page/index.html` und `unlock-email.html` von den lokalen Mockup-Dateien auf die echten Live-URLs umgestellt:

- `2-OPENLEARN/workshops.html` → `https://open-learn.app/#/deutsch`
- `2-OPENLEARN/workshop-unlocked.html` → `https://open-learn.app/#/deutsch/linux-grundlagen-preview/lessons`

Die Mockup-Dateien bleiben im Repo als Vergleichsmaterial bzw. Fallback.

## Was an diesem Plan offen ist

- Endgültiger Zugangs-Schutz: Path-as-Secret vs. signierte Tokens — wird in der Implementierung anhand des einfachsten produktiven Wegs festgelegt
- Discovery-Modell (kuratierte Premium-Liste in der App?) — getrennter späterer Plan
- Refunds und Umsatz-Verteilung — Geschäftsfragen, kein Implementierungs-Thema
