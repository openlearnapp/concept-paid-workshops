# Fallbeispiel: Bezahlter Linux-Workshop

Dieses Fallbeispiel zeigt von null bis zum fertigen Lernen, wie ein bezahlter Workshop nach
das Konzept funktioniert. Es benutzt den echten Linux-Grundlagen-Workshop, präsentiert
von einem erfundenen Kurs-Studio namens **LINUXPFAD**.

## Der Punkt dieses Fallbeispiels

Du sollst auf einen Blick sehen können: **was gehört dem Anbieter, was gehört Open Learn?**
Darum ist alles in zwei Ordner getrennt:

- `1-ANBIETER/` — alles, was das Kurs-Studio LINUXPFAD besitzt und betreibt
- `2-OPENLEARN/` — alles, was die Plattform Open Learn besitzt und betreibt

Jeder Ordner hat eine Datei `_GEHOERT-...md`, die das nochmal sagt.

## Anbieter-Seite = HTML · Open-Learn-Seite = die ECHTE App

- **`1-ANBIETER/`** — die Verkaufs-Seite ist eigenes HTML. Das ist immer so: die Landing-Page gehört dem Anbieter, hat dessen eigene Marke (hier: Terminal-Stil). Sie ist nicht Teil von Open Learn.
- **`2-OPENLEARN/`** — hier liegt **kein nachgebautes HTML**. Die Open-Learn-Seite ist die **echte, live laufende App** unter `https://open-learn.app`. Echter Lernpfad, echte Buttons, echtes Quiz, Audio, Video. Die „Kostenlos starten"- und „Kurs öffnen"-Knöpfe führen direkt dorthin — ein Klick, kein Setup.
- Das **einzige Feature, das Open Learn noch bauen muss**, ist das Schloss-Symbol auf bezahlten Lektionen — beschrieben in `specs/001-paid-workshops.md`, nicht nachgebaut.

## So klickst du das Fallbeispiel durch (0 bis Ende)

Das Fallbeispiel ist self-contained — Trailer-Videos sind eingebettet, die Open-Learn-Links
führen auf die live App. Einfach die Landing-Page öffnen, **Schritt 1 startet alles:**

| Schritt | Was du tust | Was du siehst | Wem gehört's |
|---|---|---|---|
| 1 | Landing-Page öffnen | Verkaufs-Seite: Trailer, 13 Lektionen, Preis | ANBIETER |
| 2 | „Kostenlos starten" klicken | das ECHTE Open Learn (open-learn.app) mit dem Linux-Workshop | OPEN LEARN |
| 3 | zurück, „Komplettkurs freischalten" | Stripe-ähnlicher Checkout | ANBIETER |
| 4 | „39 € bezahlen" klicken | Freischalt-Mail mit geheimem Link | ANBIETER |
| 5 | in der Mail „Kurs öffnen" klicken | das ECHTE Open Learn, voller Kurs | OPEN LEARN |

Einstieg ist immer `1-ANBIETER/landing-page/index.html`. Schritt 2 und 5 öffnen die echte,
live laufende Open-Learn-App unter `https://open-learn.app` — kein Setup, kein Server nötig.

## Was in jedem Schritt technisch passiert

1. **Landing-Page** — der Anbieter zeigt seine Verkaufs-Seite. Eigene Marke, eigener Stil, eigener Preis.
2. **Kostenlose Vorschau** — der „Kostenlos starten"-Link öffnet das echte Open-Learn-Plugin. Es lädt die öffentliche YAML (`workshop-inhalt/frei/`), die nur 2 Lektionen listet. (Mit dem Schloss-Feature würden die anderen 11 mit Schloss erscheinen — das Feature ist noch zu bauen.)
3. **Checkout** — der Kauf passiert auf der Anbieter-Seite. Open Learn ist nicht beteiligt.
4. **Freischalt-Mail** — das Verkauf-Backend des Anbieters erzeugt einen geheimen Link und mailt ihn.
5. **Vollzugang** — der Link öffnet das echte Plugin mit der geheimen YAML (`workshop-inhalt/komplett-7K2X9F4A/`), die alle 13 Lektionen listet.

Der ganze Unterschied zwischen „frei" und „bezahlt" ist: **welche YAML-URL Open Learn bekommt.**
Open Learn selbst hat keinen Bezahl-Code, keine Konten, kein Backend.

## Die Diagramme

Im Ordner `diagramme/`:

- `wem-gehoert-was.svg` — die Eigentums-Karte: Anbieter-Seite vs. Open-Learn-Seite
- `architektur.svg` — die Zwei-System-Architektur
- `anna-reise.svg` — die 6 Schritte der Käuferin Anna
- `zugang-schutz.svg` — drei Wege, Zugang ohne Backend zu schützen

## Die Videos

Trailer und Lektions-Videos kommen aus dem echten Linux-Workshop:
`workshop-linux-grundlagen/videos/`. Es gibt sie in zwei Stilen — `svgs/` (animiert) und
`comfyui/` (Comic). Auf der Landing-Page kann man oben im Trailer zwischen beiden umschalten.

## Wichtig

Dieses Fallbeispiel ist ein **Mockup zur Konzept-Diskussion**. Es ist statisches HTML/CSS,
keine echte Bezahlung, kein echtes Backend, kein Eingriff in den Open-Learn-Code. Es zeigt,
*wie* es funktionieren würde — gebaut wird erst nach Freigabe.
