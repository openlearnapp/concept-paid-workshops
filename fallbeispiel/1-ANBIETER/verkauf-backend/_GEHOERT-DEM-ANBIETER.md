# Verkauf-Backend (gehört dem Anbieter)

Das ist der einzige Teil im ganzen Fallbeispiel, der einen **Server** braucht. Und er gehört
**dem Anbieter**, nicht Open Learn. Open Learn bleibt komplett ohne Backend.

Hier steht kein Code — das Backend wird im Konzept beschrieben, nicht im Mockup gebaut.

## Was das Backend tut

Es ist eine winzige Funktion (Serverless, z.B. Cloudflare Worker oder Vercel Function). Sie macht genau drei Dinge:

1. **Zahlung empfangen.** Stripe meldet per Webhook „Anna hat 39 € bezahlt".
2. **Freischalt-Pfad erzeugen.** Das Backend würfelt einen langen Zufalls-String, z.B. `komplett-7K2X9F4A...` und legt dort (oder verlinkt) die Vollversion des Workshops ab.
3. **Mail senden.** Es schickt Anna eine Mail mit ihrem persönlichen Freischalt-Link.

## Was das Backend NICHT tut

- Es spricht **nie mit Open Learn**. Open Learn ruft dieses Backend nicht auf.
- Es speichert keine Lern-Fortschritte. Das macht Open Learn lokal beim Lerner.
- Es rendert keine Lektionen. Das macht Open Learn.

## Warum das beim Anbieter liegt und nicht bei Open Learn

Projektvorgabe: Verkauf und Freigabe passieren auf einer separaten Seite, nicht im
Lern-Plugin. Diese separate Seite darf ein Backend haben, das den Kauf verifiziert.

Jeder Anbieter bringt sein eigenes Verkauf-Backend mit — mit seinem eigenen Stripe-Konto.
Die Open-Learn-Library kann eine fertige Vorlage dafür anbieten, damit Anbieter es nicht
von Null bauen müssen. Aber betrieben wird es vom Anbieter.

## Ablauf als Skizze

```
Anna bezahlt 39 EUR
        │
        ▼
Stripe ──webhook──►  Verkauf-Backend des Anbieters
                          │
                          ├─ erzeugt geheimen Pfad  komplett-7K2X9F4A
                          │
                          └─ sendet Mail mit Link an Anna
                                     │
                                     ▼
                          Anna klickt Link
                                     │
                                     ▼
                          Open Learn laedt die geheime YAML-URL
                          und rendert alle 13 Lektionen
```

Open Learn taucht erst im letzten Schritt auf — als Player. Vorher ist alles Anbieter-Sache.
