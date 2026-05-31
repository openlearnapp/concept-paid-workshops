# Die OPEN-LEARN-Seite = die echte, live laufende App

Hier liegt **kein nachgebautes HTML**. Die Open-Learn-Seite des Fallbeispiels ist die
**echte Open-Learn-App** — sie ist bereits live im Internet.

## So siehst du sie — ohne irgendwas zu installieren

Open Learn läuft öffentlich unter **https://open-learn.app**.

Die „Kostenlos starten"- und „Kurs öffnen"-Knöpfe auf der Anbieter-Landing-Page
(`1-ANBIETER/landing-page/`) führen direkt dorthin — ein Klick, kein Setup.

## Was die echte App schon kann

Echter Lernpfad, echte Lektionen, echtes Quiz, Audio, Video, Fortschritt — alles live.

## Premium-Funktion (in Umsetzung)

Die App lernt gerade das, was im Konzept beschrieben ist — als Plattform-Funktion in
`openlearnapp/openlearnapp.github.io`. Jeder Anbieter kann dann in seiner
`workshops.yaml` selbst entscheiden:

- **Kostenlos** — wie bisher, kein Banner, keine Schlösser
- **Komplett Premium** — alle Lektionen gesperrt, Verkaufs-Banner ganz oben
- **Premium mit freier Vorschau** — einzelne Lektionen frei (Anbieter wählt welche), Rest gesperrt
- **Video-Lock pro Lektion** (geplant) — eine Lektion ist textlich frei, aber Videos sind gesperrt

Status der PRs:

- ✅ Bot-Refactor als Vorbereitung — `openlearnapp/openlearnapp.github.io` PR #292 gemerged
- 🟡 Premium-Backbone (Schema + Banner + Schloss-Karten + URL-Guard) — `openlearnapp/openlearnapp.github.io` PR #294 offen
- ⏳ Premium-Indikator auf Workshop-Karten — Folge-PR
- ⏳ Anbieter-Onboarding auf Startseite — Folge-PR
- ⏳ Creators-Seite Cinematic Redesign — Folge-PR
- ⏳ Video-Lock pro Lektion — Folge-PR

## Warum hier kein nachgebautes HTML liegt

Open Learn existiert schon als laufende, öffentlich erreichbare App. Sie nachzubauen wäre
Verschwendung. Die echte App unter open-learn.app ist die Open-Learn-Seite des Fallbeispiels.
