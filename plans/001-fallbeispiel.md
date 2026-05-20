# Plan: Fallbeispiel-Aufbau

Wie das Fallbeispiel im Ordner `fallbeispiel/` aufgebaut ist und welche Schritte folgen.

## Leitidee

Das Fallbeispiel trennt physisch, was getrennt sein muss: zwei Ordner, `1-ANBIETER/` und
`2-OPENLEARN/`. Jeder, der reinschaut, soll sofort wissen, welcher Teil wem gehört. Die
zwei Welten sehen auch optisch komplett verschieden aus.

## Demo-Workshop

Der echte Linux-Grundlagen-Workshop (13 Lektionen), präsentiert vom erfundenen Kurs-Studio
LINUXPFAD. Erste 2 Lektionen frei, restliche 11 bezahlt.

| # | Lektion | Status |
|---|---|---|
| 01 | Wie funktioniert ein Computer? | frei |
| 02 | Was ist Linux? | frei |
| 03 | Das Terminal — erste Schritte | bezahlt |
| 04 | Dateien & Ordner | bezahlt |
| 05 | Dateiinhalt | bezahlt |
| 06 | Berechtigungen | bezahlt |
| 07 | Prozesse | bezahlt |
| 08 | Paketverwaltung | bezahlt |
| 09 | Netzwerk | bezahlt |
| 10 | Shell Scripting Basics | bezahlt |
| 11 | Vim & Texteditoren | bezahlt |
| 12 | Systeminformationen | bezahlt |
| 13 | Professioneller Linux-Workflow | bezahlt (Abschluss) |

## Aufbau

```
fallbeispiel/
├── README.md                  Durchklick-Anleitung 0 bis Ende
├── diagramme/                 4 SVG-Diagramme
├── 1-ANBIETER/                gehoert dem Kurs-Studio LINUXPFAD
│   ├── landing-page/          Verkaufs-Seite, Checkout, Freischalt-Mail,
│   │                          eingebettete Trailer-Videos
│   ├── workshop-inhalt/       YAML — frei (2 Lekt.) + komplett (13 Lekt.)
│   └── verkauf-backend/       Beschreibung des Kauf-Servers
└── 2-OPENLEARN/               gehoert der Plattform Open Learn
    └── _GEHOERT-OPENLEARN.md  Verweis auf die echte, live laufende App
                               (open-learn.app) — kein Nachbau
```

## Zwei optische Welten (Absicht)

- **Anbieter (LINUXPFAD)** — Terminal-Stil: fast schwarz, Terminal-Grün, Monospace. Eigene
  Marke des Anbieters.
- **Open Learn** — die echte, live laufende App: Cinematic-Stil, tiefes Blau-Violett. Für
  alle Workshops gleich.

So sieht man ohne Nachdenken, in welcher Welt man gerade ist.

## Videos

Die Trailer-Videos (Lektion 01 in zwei Stilen — SVG-animiert und Comic) sind in die
Landing-Page eingebettet: `1-ANBIETER/landing-page/assets/videos/`. Damit ist das Fallbeispiel
self-contained und ohne externe Pfade live abspielbar. Die vollständigen Lektions-Videos
liegen im Linux-Workshop-Repo und sind nicht Teil dieses Konzept-Repos.

## Was das Fallbeispiel zeigt — und was nicht

Zeigt:
- Die komplette Käufer-Reise von der Verkaufs-Seite bis zum freigeschalteten Kurs.
- Die saubere Trennung zwischen Anbieter und Open Learn.
- Wie „frei" und „bezahlt" allein über zwei YAML-URLs funktioniert.

Zeigt nicht:
- Echte Stripe-Integration, echtes Backend, echte Mails.
- Eingriffe in den Open-Learn-Produktiv-Code.

Alles ist statisches HTML/CSS/SVG, läuft im Browser, kein Build, keine Implementation.

## Folge-Schritte

1. Lokaler Test des Fallbeispiels.
2. Konzept-Repo auf GitHub bereitstellen.
3. PR mit dem Konzept zur Review öffnen.
4. Review-Iterationen am Spec-Dokument (erwartet 2–3 Runden).
5. Nach Konsens: eigener Plan für die Library-Erweiterung und die zwei Open-Learn-UI-Änderungen.
6. Implementierung erst nach explizitem Go.
