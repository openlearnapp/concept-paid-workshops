# Analyse 000 — Stand und offene Fragen

Auswertung der Konzept-Arbeit für bezahlte Workshops. Stand: 2026-05-20.

## Auftrag

Ein Konzept für bezahlte Workshops auf Open Learn:

- Öffentliche Vorschau-Lektionen + bezahlte Lektionen (Preview frei, Rest mit Zugang)
- Zugang ohne Backend in Open Learn
- Verkauf und Freigabe auf einer separaten Seite, nicht im Lern-Plugin
- Konzept zuerst als PR, mehrere Iterationen, Implementation erst danach
- Eigenes Repo mit der Struktur Specs / Plans / Analysis

## Was gebaut wurde

| Pfad | Inhalt |
|---|---|
| `specs/001-paid-workshops.md` | Das Konzept (Architektur, drei Zugangs-Optionen, offene Fragen) |
| `plans/001-fallbeispiel.md` | Aufbau des Fallbeispiels |
| `fallbeispiel/1-ANBIETER/` | Landing-Page, Checkout, Freischalt-Mail, Workshop-YAML (frei + komplett) |
| `fallbeispiel/2-OPENLEARN/` | Pointer auf die echte Open-Learn-App — kein Nachbau |
| `fallbeispiel/diagramme/` | Vier Diagramme: Eigentum, Architektur, Käufer-Reise, Zugangs-Schutz |
| `WEM-GEHOERT-WAS.md` | Klärung: was gehört dem Anbieter, was Open Learn |

Das Fallbeispiel: ein erfundenes Studio „LINUXPFAD" verkauft den echten Linux-Workshop.
Durchklickbar von der Verkaufs-Seite bis in das echte Open-Learn-Plugin.

## Auswertung — was steht

- **Zwei-System-Architektur ist klar:** Anbieter verkauft auf eigener Landing-Page,
  Open Learn rendert. Geld fließt nie durch Open Learn.
- **Frei/bezahlt funktioniert über zwei YAML-Einstiegspunkte:** die öffentliche `frei/`-YAML
  listet die Vorschau-Lektionen, die geheime `komplett-<secret>/`-YAML listet alle. Open Learn
  rendert nur, was die Liste enthält — kein Bezahl-Code nötig.
- **Die echte Open-Learn-App rendert den Workshop bereits** — ohne eine Zeile neuen Code.
- **Open Learn braucht für bezahlte Workshops nur eine Mini-Änderung:** ein Schloss-Symbol
  auf Lektionen, die nicht in der geladenen YAML stehen.

## Auswertung — was von Felix' Antworten abhängt

Sechs Punkte sind noch offen. Sie betreffen Entscheidungen, die das Konzept nicht allein
treffen kann — sie brauchen Felix.

## Offene Fragen

1. **Vorschau-Umfang** — Fest Lektion 1–3 frei, oder entscheidet jeder Anbieter selbst?
2. **Zugang ohne Backend** — Welche Variante: (A) geheime URL, (B) signierte Tokens,
   (C) verschlüsselte Inhalte? Keine verhindert die Weitergabe des Links zu 100 % — ist das
   für den Start akzeptabel?
3. **Verkauf separat** — Bestätigung: Workshop-Anzeige bleibt in Open Learn wie gebaut, nur
   Bezahlung/Freischaltung läuft über die separate Landing-Page. Und: ist das Schloss-Symbol
   als einzige Mini-Änderung in Open Learn ok?
4. **Freischalt-Link** — Was war mit „Trödelmarkt" gemeint?
5. **Library** — Bestätigung, dass wir `open-learn.js` erweitern. Soll sie auch eine
   Backend-Vorlage für den Kauf mitbringen?
6. **Konzept-Repo** — Auf GitHub unter der openlearnapp-Org oder unter Rezas Account?

## Nächste Schritte

1. Fragen mit Felix klären (Nachricht ist gestellt).
2. Konzept-Repo auf GitHub bereitstellen, damit Felix alles durchklicken kann.
3. Nach Felix' Antworten das Konzept **sofort** überarbeiten.
4. Erwartet: 2–3 Iterationen, bis das Konzept implementierbar ist.
5. Implementation erst nach Felix' ausdrücklicher Freigabe.
