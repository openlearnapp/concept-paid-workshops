# Spec 002 — Open-Learn-Mockup-Seiten im Fallbeispiel

## Zweck

Das Fallbeispiel zeigt den vollständigen Kauf-Flow eines bezahlten Workshops — von der Anbieter-Verkaufs-Seite über Checkout und Freischalt-Mail bis in die Lern-App. Bis die echten App-Erweiterungen produktiv sind, simulieren statische HTML-Seiten den Open-Learn-Teil. So ist der Flow durchklickbar, ohne dass die Plattform schon angepasst sein muss.

## Was die Mockup-Seiten zeigen

| Datei | Was sie darstellt |
|---|---|
| `fallbeispiel/2-OPENLEARN/workshops.html` | Workshop-Übersicht in Open Learn, Premium-Workshop visuell hervorgehoben |
| `fallbeispiel/2-OPENLEARN/workshop-preview.html` | Lernpfad eines Premium-Workshops vor dem Kauf — 2 freie Lektionen, restliche mit Schloss-Symbol |
| `fallbeispiel/2-OPENLEARN/workshop-unlocked.html` | Lernpfad nach dem Kauf — alle Lektionen offen |
| `fallbeispiel/2-OPENLEARN/style.css` | Gemeinsame Styles im Open-Learn-Look |

## Anbindung an den Anbieter-Teil

Die Anbieter-Landing-Page (`fallbeispiel/1-ANBIETER/landing-page/index.html`) verlinkt direkt auf `2-OPENLEARN/workshops.html`. Die Freischalt-Mail (`unlock-email.html`) verlinkt auf `workshop-unlocked.html`. So entsteht ein vollständig durchklickbarer Kauf-Flow ohne Backend.

## Verhältnis zur echten Plattform

Diese Mockups sind **temporär**. Die produktive Lösung läuft auf der echten Open-Learn-App, sobald die Premium-Workshop-Erweiterung dort verfügbar ist. Details: siehe `plans/002-integration-in-open-learn.md`.

Wenn die echte App das Premium-System rendert, werden die Anbieter-Links in einem Folge-Commit von den Mockup-Seiten auf die Live-URLs umgestellt.

## Was die Mockups bewusst NICHT zeigen

- Checkout-Backend (Stripe/Lemon Squeezy etc.) — Konzept-Annahme: läuft auf der Anbieter-Domain
- Account-System auf Open-Learn-Seite — Konzept-Annahme: kein Account, Freischaltung per Token in URL
- Mehrsprachigkeit — Mockups nur Deutsch
