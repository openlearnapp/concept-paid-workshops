# Workshop-Inhalt (gehört dem Anbieter)

Der Anbieter hostet seinen Kurs als YAML. Für bezahlte Workshops gibt es **zwei Einstiegspunkte** — der Trick, mit dem „frei" und „bezahlt" ohne Backend in Open Learn funktioniert.

## Die zwei Einstiegspunkte

### `frei/` — die öffentliche Vorschau

- Liegt unter einer **öffentlichen, leicht zu erratenden URL**, z.B. `linuxpfad.github.io/linux-grundlagen/index.yaml`
- Die `lessons.yaml` listet **nur die 2 kostenlosen Lektionen**
- Jeder darf diese URL nutzen — sie ist die Vorschau

### `komplett-7K2X9F4A/` — die freigeschaltete Vollversion

- Liegt unter einer **geheimen, nicht erratbaren URL**, z.B. `linuxpfad.github.io/linux-grundlagen/komplett-7K2X9F4A/index.yaml`
- Die `lessons.yaml` listet **alle 13 Lektionen**
- Der Pfad-Teil `7K2X9F4A` ist im Fallbeispiel kurz. In echt wäre er ein langer Zufalls-String, vom Verkauf-Backend pro Käufer erzeugt.

## Warum das funktioniert

Open Learn lädt einfach die URL, die es bekommt:

- Vorschau-Link → lädt `frei/` → Open Learn zeigt 2 Lektionen
- Freischalt-Link → lädt `komplett-7K2X9F4A/` → Open Learn zeigt 13 Lektionen

Open Learn muss **nicht wissen**, ob jemand bezahlt hat. Es rendert nur, was die `lessons.yaml` auflistet. Die Zugangskontrolle steckt darin, **wer die geheime URL kennt** — und die bekommt nur, wer gekauft hat.

Das ist „Option A — Path-as-Secret" aus `specs/001-paid-workshops.md`.

## Hinweis zum Lektions-Inhalt

Die eigentlichen Lektions-Dateien (`content.yaml` pro Lektion) liegen im echten Workshop-Repo
`workshop-linux-grundlagen/`. Hier im Fallbeispiel zeigen wir nur die **Struktur-Dateien**
(`index.yaml`, `workshops.yaml`, `lessons.yaml`), weil genau dort der Unterschied zwischen
frei und komplett sichtbar wird: in der Liste der Lektionen.
