# Wem gehört was?

Die wichtigste Frage beim Konzept für bezahlte Workshops: **Welcher Teil gehört dem Kurs-Anbieter, welcher Teil gehört Open Learn?** Solange das nicht glasklar ist, kann man nichts sauber implementieren.

Dieses Dokument beantwortet das. Das Fallbeispiel im Ordner `fallbeispiel/` ist genau danach aufgebaut: zwei physisch getrennte Ordner, `1-ANBIETER/` und `2-OPENLEARN/`.

## Die zwei Welten

### Welt A — Der Anbieter (im Fallbeispiel: das Studio „LINUXPFAD")

Der Anbieter ist eine fremde Person oder Firma, die einen Kurs verkaufen will. Im Fallbeispiel ist das ein erfundenes Linux-Kurs-Studio namens LINUXPFAD. Es benutzt den echten Linux-Grundlagen-Workshop als Inhalt.

Der Anbieter **besitzt und betreibt**:

| Teil | Was es ist | Liegt im Ordner |
|---|---|---|
| Workshop-Inhalt | Die YAML-Dateien mit Lektionen, Fragen, Videos | `1-ANBIETER/workshop-inhalt/` |
| Landing-Page | Die Verkaufs-Seite mit eigenem Marken-Stil | `1-ANBIETER/landing-page/` |
| Verkauf-Backend | Der kleine Server, der Käufe prüft und Links erzeugt | `1-ANBIETER/verkauf-backend/` |
| Eigene Marke | Farben, Logo, Tonfall, Preisgestaltung | überall in `1-ANBIETER/` |
| Hosting | GitHub Pages, eigener Server, IPFS — der Anbieter wählt | — |
| Geld | Der Anbieter kassiert direkt, behält 100 % | — |

### Welt B — Open Learn (die Plattform)

Open Learn ist die kostenlose Lern-App. Sie **besitzt und betreibt**:

| Teil | Was es ist | Wo |
|---|---|---|
| Der Renderer | Das Programm, das jede Workshop-YAML in einen Kurs verwandelt | echte App, `open-learn.app` |
| Einheitlicher Lern-Stil | Alle Kurse sehen im Lern-Bereich gleich aus | echte App, `open-learn.app` |
| Lern-Funktionen | Quiz, Audio, Video-Player, Fortschritt, Coach | echte App, `open-learn.app` |
| Die Library | Die geteilte Datei `open-learn.js` für alle Landing-Pages | im echten Open-Learn-Repo |

Im Fallbeispiel-Ordner `2-OPENLEARN/` liegt darum kein Nachbau — nur ein Verweis auf die
echte, live laufende App.

Open Learn **wickelt das Geld nicht ab** (das macht der Anbieter auf seiner Seite), **kann aber
an bezahlten Workshops mitverdienen** — siehe unten.

## Die Trennlinie in einem Satz

> Der Anbieter besitzt **Roh-Inhalt, Verkauf und Marke**. Open Learn besitzt **das Lernerlebnis** —
> die reiche Darstellung (Story-Mode, Lernpfad, Quiz, Audio), die aus Roh-Inhalt erst einen
> verkaufbaren Kurs macht.

## Warum Anbieter Open Learn nutzen — und was Open Learn davon hat

Open Learn ist **kein passiver Player**. Der Anbieter liefert nur Roh-Inhalt: YAML-Text und
Videos. Open Learn macht daraus das, was man verkaufen kann — einen Story-Mode-Kurs mit
Lernpfad, Quiz, Audio, Fortschritt, Synchronisation. Diese Verwandlung ist der Mehrwert.

Daraus folgt das Geschäftsmodell:

- Der Anbieter **bietet seinen Kurs über Open Learn an** — präsentiert im Open-Learn-Lernerlebnis.
- **Verkauft** wird auf einer separaten Seite (Felix' Vorgabe: Verkauf ist nicht im Lern-Plugin).
- Das **Verkaufen ist ein Feature**, das die Open-Learn-Welt bereitstellt — und genau dafür
  **kann Open Learn einen Anteil am Verkauf nehmen**.

So verdient Open Learn mit: nicht weil es Geld abwickelt, sondern weil es die Darstellung
liefert, die den Kurs überhaupt verkaufbar macht, und das Verkaufen als Feature ermöglicht.

## Wie die Daten fliessen

```
ANBIETER                                          OPEN LEARN
────────                                          ──────────

workshop-inhalt/  ──── YAML per URL ───────────►  Renderer liest YAML
(Lektionen)                                       und zeigt den Kurs

landing-page/     ──── Käufer klickt ──────────►  Renderer öffnet
(Verkaufs-Seite)       Freischalt-Link            mit der Unlock-URL

verkauf-backend/  ──── prüft Stripe-Zahlung       (Open Learn sieht
(Kauf-Prüfung)         erzeugt Freischalt-Link     davon nichts)
```

Open Learn bekommt vom Anbieter immer nur **eine URL**. Was dahinter steckt — frei oder bezahlt — ist Sache des Anbieters. Open Learn lädt die URL und rendert. Mehr nicht.

## Was der Anbieter tun muss, damit sein Kurs verkauft und gezeigt werden kann

Sechs Schritte. Alle gehören dem Anbieter:

1. **Inhalt schreiben** — Kurs als YAML nach Open-Learn-Struktur (Sprache → Workshop → Lektionen → Sektionen → Beispiele).
2. **Zwei Einstiegspunkte hosten** — eine öffentliche `index.yaml` mit nur den Vorschau-Lektionen, und eine `index.yaml` unter geheimem Pfad mit allen Lektionen.
3. **Landing-Page bauen** — mit der Open-Learn-Library, im eigenen Marken-Stil.
4. **Verkauf-Backend aufsetzen** — kleine Serverless-Funktion, die Stripe-Zahlungen prüft.
5. **Freischalt-Mechanik** — nach erfolgreicher Zahlung erzeugt das Backend einen geheimen Link und mailt ihn dem Käufer.
6. **Werben** — der Anbieter macht selbst Werbung für seine Landing-Page. Open Learn hat keine Such- oder Marktplatz-Funktion.

## Was Open Learn dafür braucht (minimal)

Nur zwei kleine Dinge im Renderer:

1. **Schloss-Symbol** auf Lektionen, die in der geladenen YAML nicht enthalten sind.
2. **Hinweis-Karte** bei Klick auf eine gesperrte Lektion, die zur Landing-Page des Anbieters zurückführt.

Kein Bezahl-Code, keine Konten, kein Backend in Open Learn.

## Warum die zwei Stile im Fallbeispiel so verschieden aussehen

Das ist Absicht. Damit man sofort sieht, wo man ist:

- **Anbieter-Seite (LINUXPFAD)** — Terminal-Stil: fast schwarz, Terminal-Grün, Monospace-Schrift. Sieht aus wie das Produkt eines Entwickler-Studios.
- **Open Learn** — Cinematic-Stil: tiefes Blau-Violett, Aurora-Verläufe, weiche Rundungen. Sieht aus wie die Plattform.

Im echten Betrieb wählt jeder Anbieter seinen eigenen Stil für seine Landing-Page. Der Lern-Bereich in Open Learn bleibt für alle gleich.
