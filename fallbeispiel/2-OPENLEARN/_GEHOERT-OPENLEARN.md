# Die OPEN-LEARN-Seite = die echte, live laufende App

Hier liegt **kein nachgebautes HTML**. Die Open-Learn-Seite des Fallbeispiels ist die
**echte Open-Learn-App** — und die ist bereits live im Internet.

## So siehst du sie — ohne irgendwas zu installieren

Open Learn läuft öffentlich unter **https://open-learn.app**. Der Linux-Workshop ist dort
schon verfügbar:

```
https://open-learn.app/#/deutsch/linux-grundlagen/lessons
```

Die „Kostenlos starten"- und „Kurs öffnen"-Knöpfe auf der Anbieter-Landing-Page
(`1-ANBIETER/landing-page/`) führen genau dorthin — ein Klick, kein Setup.

## Was die echte App schon kann

Echter Lernpfad, echte Lektionen, echtes Quiz, Audio, Video, Fortschritt — alles live.
Sie rendert den echten Linux-Workshop ohne eine Zeile neuen Code.

## Was der echten App für bezahlte Workshops noch fehlt

Genau **zwei kleine Dinge** — das ist alles, was Open Learn implementieren müsste:

1. **Schloss-Symbol** auf Lektionen, die in der geladenen YAML nicht enthalten sind.
2. **Hinweis-Karte** bei Klick auf eine gesperrte Lektion, die zur Anbieter-Landing-Page führt.

Diese zwei Punkte sind im Konzept (`specs/001-paid-workshops.md`) beschrieben. Sie werden
erst nach Felix' Freigabe gebaut — nicht vorher.

## Warum hier kein nachgebautes HTML liegt

Open Learn existiert schon als laufende, öffentlich erreichbare App. Sie nachzubauen wäre
Verschwendung. Die echte App unter open-learn.app ist die Open-Learn-Seite des Fallbeispiels.
