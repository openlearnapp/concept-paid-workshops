# Plan 002 — Integration in die echte Open-Learn-App

## Ziel

Das Konzept aus `specs/001-paid-workshops.md` in der produktiven Open-Learn-App umsetzen. Open Learn lernt eine **Plattform-Funktion** kennen: jeder Anbieter kann in seiner eigenen `workshops.yaml` selbst entscheiden, ob sein Workshop kostenlos, ganz Premium oder mit freier Vorschau angeboten wird. Kein extra Repo, kein Nachbau — die Anpassung lebt in der App selbst.

## Was Anbieter entscheiden können

Drei Modi, alle in `workshops.yaml`:

| Modus | Feld(er) |
|---|---|
| Kostenlos (wie heute) | `premium:` weggelassen oder `false` |
| Komplett Premium | `premium: true` + kein `free_lessons` |
| Premium mit Vorschau | `premium: true` + `free_lessons: N` **oder** `free_lesson_numbers: [a, b, c]` |
| Pro-Video-Lock innerhalb einer Lektion | `section.video.premium: true` — Folge-Implementierung |

Plus `provider:` Block (Logo, Headline, Pitch, Bullets, `landing_url`, `accent_color`, Preis-Anzeige) für Branding und Verkaufs-CTA.

## Aufteilung in PRs

Die Implementierung läuft im Plattform-Repo `openlearnapp/openlearnapp.github.io`, ein PR pro Sektion:

1. **Bot-Refactor (Voraussetzung)** — Quizze ruhig inline statt animierter Roboter — [PR #292](https://github.com/openlearnapp/openlearnapp.github.io/pull/292), gemerged 2026-05-31
2. **Premium-Backbone** — Schema + Anbieter-Werbe-Banner + Schloss-Lektionen + URL-Guard — [PR #294](https://github.com/openlearnapp/openlearnapp.github.io/pull/294), offen
3. **Premium-Indikator auf Workshop-Karten** — Aurora-Rand + Stern-Badge + Anbieter-Strip in der Workshop-Liste — Folge-PR
4. **Anbieter-Onboarding auf der Startseite** — Erklär-Sektion „Verkaufe deinen Kurs über Open Learn" mit YAML-Snippet — Folge-PR
5. **Creators-Seite Cinematic Redesign** — vollständige Premium-Sektion mit Live-Demo-Verweis — Folge-PR
6. **Video-Lock pro Lektion** — `section.video.premium: true`, Vorschau-Bild statt Player wenn gesperrt — Folge-PR

## Wo Felix die Änderungen sieht

Nach Merge der jeweiligen PRs direkt auf **https://open-learn.app/**. Jeder Workshop-Anbieter, der `premium: true` in seine `workshops.yaml` setzt, bekommt automatisch das Premium-Rendering — Banner, Schlösser, Guard, Werbe-Inhalt.

Bis zum Merge testet Reza lokal über `pnpm dev`.

## Was kein Bestandteil der Implementierung ist

- Kein Account-System, kein Login
- Kein Open-Learn-eigener Checkout — der Kauf passiert beim Anbieter
- Keine Umsatzbeteiligung in der App selbst — Geschäftsfrage, kein Code

## Offene Punkte für Folge-Iterationen

- Endgültiger Zugangs-Schutz nach Kauf — Path-as-Secret vs. signierte Tokens
- Auto-Unlock per `?unlock=<token>` URL-Parameter — `unlock_token`-Feld im Schema ist dafür reserviert
- Discovery-Modell — getrennter späterer Plan
