# ⚽ Quiz-Fussball Live — Konzept (v1.0)

## Idee in einem Satz
Zwei Teams treten live gegeneinander an: pro Frage ein Duell — das schnellere Team
mit zwei richtigen Antworten schiebt einen gemeinsamen Ball einen Schritt Richtung
gegnerisches Tor. Ball im Tor = ein Treffer. Am Beamer wandert der Ball **live**
übers Spielfeld, auf den Handys wird geantwortet.

---

## Kern-Mechanik (festgelegt)
- **Ein gemeinsamer Ball, Tauziehen-Prinzip.**
- **Frage für Frage, Punkt für Punkt:** Jede Frage ist ein eigenes Duell. Das Team,
  das **zuerst 2 richtige Antworten** hat, **gewinnt die Frage** → Ball **1 Schritt**
  Richtung gegnerisches Tor. Danach **sofort eine neue Frage** für beide gleichzeitig.
  **Kein Weiterspielen** nach gewonnener Frage (Sieger bekommt keinen Bonus).
- **Kein Timer.** Es zählt nur Korrektheit + wer **schneller** zwei Richtige hat.
- **Faire Zeitmessung auf dem Gerät:** Jede Antwort misst die **Reaktionszeit ab
  Einblenden der Frage** (lokal auf dem Handy → unabhängig vom Internet-Tempo).
  Die „Zeit" eines Teams = Reaktionszeit seiner **2. richtigen** Antwort. Kürzere
  Zeit gewinnt die Frage. (Exakt gleich = Ball bleibt stehen.)
- **Spielende:** der Host beendet das Match **individuell per „Schlusspfiff"**.

---

## Spielfeld & Live-Visualisierung (Beamer = Herzstück)

```
[ TOR A ]  ◀  2 — 1 — ( ⚽ MITTE ) — 1 — 2  ▶  [ TOR B ]
```

- Ball startet in der **Mitte**. **2 Schritte** pro Seite bis zum Tor (kurzes Feld →
  viele Treffer).
- Gewinnt ein Team eine Frage → der Ball **gleitet sichtbar (animiert) 1 Feld**
  Richtung gegnerisches Tor.
- Ball erreicht ein Tor → **TREFFER-Animation**, Anzeigetafel +1, Ball zurück in die Mitte.
- Am Beamer zu sehen: **Spielfeld mit aktueller Ballposition** (live), **Trefferstand
  A : B**, und die **aktuelle Frage** zum Mitlesen. *Keine Quoten/Statistik.*

> Das kurze Feld + „jede Frage ein frisches, gleichberechtigtes Duell" ist zugleich
> der **Ausgleich**: kein Team kann davonrennen, das langsamere bekommt jede Frage
> eine neue Chance.

---

## Ablauf einer Frage
1. Host startet die nächste Frage → erscheint **gleichzeitig** bei beiden Teams und
   am Beamer.
2. Pro Team sind **N Spieler „auf dem Feld"** (aktiv) — N = Host-Einstellung (1 oder 2).
3. Jede:r aktive Spieler:in beantwortet auf dem Handy; Reaktionszeit wird lokal gemessen.
4. **Auswertung pro Team:** sobald **2 richtige** Antworten vorliegen, ist das Team fertig.
   *(Bei Einstellung „1 aktiv": eine richtige Antwort entscheidet.)*
   - Eine Antwort **falsch** → **sofort Ersatz**: die/der nächste Mitspieler:in rückt
     nach und beantwortet dieselbe Frage (kostet Zeit!).
5. **Erstes Team mit genügend Richtigen gewinnt** → Ball 1 Schritt Richtung Gegner.
   Die Frage ist damit beendet (auch fürs andere Team).
6. **Sofort neue Frage.** Aktive Spieler **rotieren**, damit alle drankommen.

---

## Teams, Rotation, Klassengrössen
- Teamzuteilung **zufällig** beim Login (wie Escape). Ungleiche Teamgrössen ok.
- Pro Frage **N Aktive pro Team** (Einstellung), reihum durch die ganze Mannschaft.
- **Ersatz** bei Fehler = nächste:r in der Reihe; ist die Mannschaft „durch",
  beginnt die Reihe von vorne.
- **Mitlesen:** **alle** Spieler sehen die Frage, aber nur die gerade **Aktiven**
  können absenden.

---

## Fragen
- **Nur Single-Choice** (genau eine richtige Antwort) in v1 → eindeutig + schnell.
- **Reihenfolge fix** wie eingegeben.
- Fragen werden als **JSON importiert / im Editor erstellt** (wie Escape/WWM).
- *Text/Zahl als spätere Erweiterung möglich.*

---

## Host-Einstellungen
- **Aktive Spieler pro Frage:** 1 oder 2 (Standard **2**).
- **Match-Steuerung:** Spiel starten · (Fragen laufen automatisch nacheinander) ·
  **Schlusspfiff** (beendet + zeigt Sieger) · Trefferstand bei Bedarf korrigieren.
- Trefferstand-Anzeige immer am Beamer.
- Gleichstand beim Schlusspfiff → **„Unentschieden"**.

---

## Rollen & Geräte (wie WWM / Escape)
- **Host** (Lehrperson, Laptop): Einstellungen, startet Fragen, beendet das Match.
- **Beamer / Display:** Live-Spielfeld + Ball + Trefferstand + aktuelle Frage.
- **Spieler** (Handys): Login mit Name → Zufalls-Team → beantworten Fragen.

---

## Technische Wiederverwendung
- **Netzwerk/Broker:** identisch zu WWM/Escape (PeerJS + `wwm-peer-broker.onrender.com`),
  inkl. `PEER_CONFIG`-Block für die Weitergabe.
- **Drei Seiten:** `host.html` (Steuerung), `display.html` (Beamer), `player.html`
  (Handys) — Muster aus WWM.
- **Eigenes GitHub-Repo + GitHub Pages.**

---

## Bau-Plan (Vorschlag der Reihenfolge)
1. **Repo + Grundgerüst** anlegen (host/display/player + Broker/PEER_CONFIG, Login & Zufallsteam).
2. **Fragen-Import + Single-Choice-Anzeige** auf den Handys.
3. **Runden-Logik:** Aktive bestimmen, Antworten + Reaktionszeit sammeln, Sieger
   einer Frage ermitteln (2 Richtige, schnellere Zeit), Ersatz-Mechanik.
4. **Beamer-Live-Visualisierung:** Ball animiert bewegen, Treffer, Trefferstand.
5. **Host-Einstellungen + Schlusspfiff + Endstand.**
6. **Test + Feinschliff** (Rotation, ungleiche Teams, Reconnect).

---

## ✅ Alles Wesentliche geklärt — bereit für die Umsetzung
*Status: v1.0. Nächster Schritt: Repo anlegen und mit Bau-Plan Schritt 1 starten.*
