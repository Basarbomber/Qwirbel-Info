<!-- Erstellt mit Qwirbel (KI-Assistent) am 03.11.2026 mit glm-5.3 ueber zai (Cloud-API) – KI-generierter Inhalt, Kennzeichnung nach Art. 50 EU-KI-VO. -->
# Qwirbel Modell-Benchmark — Arbeitsproben

**Wie gut ist ein Sprachmodell wirklich? Nicht schön reden — Aufgaben lösen.**
Qwirbel misst das jede Nacht mit echten Agent-Aufträgen. Dieser Bericht
zeigt die Zahlen ungekürzt, inklusive der Läufe, die schlecht ausgingen.

Stand: **03.11.2026** — 87 Läufe, 23 Modelle, alles auf derselben Maschine
(Ryzen 7 5700X, Radeon RX 9060 XT 16 GB, Windows 11, Ollama).

---

## Wie gemessen wird

Eine Arbeitsprobe ist kein Quiz. Das Modell läuft als voller Agent mit den
echten Qwirbel-Werkzeugen (Dateien, Shell, Python, ffmpeg, Blender und
Blockbench über MCP, Web) und bekommt 25 Aufträge:

| Feld | Aufgaben (Auswahl) |
|---|---|
| Video | schneiden + skalieren, Untertitel einbrennen, 9:16-TikTok-Format, GIF-Vorschau |
| Bild | Foto auf Webgröße bringen und prüfen |
| 3D | sechs Mobs als .glb in Blender (Skorpion, Ameise, Eis-Geist, Vulkan-Wurm, Sakura-Geist), einen Hasen nachbessern, freies Blender-Modell, Blockbench-Modell |
| Code | Python-Skript schreiben UND selbst ausführen, gezielter Bugfix in fremdem Code, Spielmodus erweitern, Minecraft-Luau |
| Web & Daten | kleine Website mit Login + Admin-Panel, Festplatte analysieren, Alltagsdaten auswerten, Maven-Link finden, Modpack prüfen |
| Organisation | zwei Aufträge in einem Chat, TikTok-Upload-Entwurf, fünf Verständnisfragen |

**Bestanden ist eine Aufgabe nur, wenn das Ergebnis auf der Platte stimmt**
(clip.mp4 wirklich 720 px hoch, .glb wirklich vorhanden, das Skript wirklich
gelaufen). „Ich bin fertig“ ohne Datei zählt nicht. Zeitlimit je Aufgabe:
40 Minuten.

---

## Aktuelle Runde: die Dauerprobe (seit 01.11.2026)

Drei Modelle laufen Nacht für Nacht im Kreis — dieselben 25 Aufgaben, jede
Runde frisch:

| Modell | Wann | Bestanden | Laufzeit |
|---|---|---|---|
| bonsai-2:27b | 03.11. 09:32 | **4/16**\* | 25.379 s |
| bonsai-2:27b | 03.11. 02:12 | 4/25 | 17.868 s |
| bonsai-2:27b | 02.11. 04:40 | 4/25 | 15.729 s |
| bonsai-2:27b | 03.11. 00:16 | 1/8 | 3.167 s |
| qwen3.5:9b | 03.11. 08:30 | 1/25 | 3.618 s |
| ternary-nemotron-30b-a3b | 02.11. 09:04 | 1/25 | 4.255 s |
| ternary-nemotron-30b-a3b | 02.11. 03:22 | 1/25 | 4.624 s |
| qwen3.5:9b | 02.11. 23:53 | 0/25 | 1.164 s |
| ternary-nemotron-30b-a3b | 03.11. 07:12 | 0/25 | 4.597 s |

\* Abbruch nach 16 Aufgaben — der Besitzer spielte gerade. Die Testkette gibt
die Grafikkarte freiwillig frei und macht nach der Pause weiter.

Bestanden hat bonsai-2:27b zuletzt: Video-Schnitt, Bild-Aufgabe,
GIF-Erzeugung und die Verständnisfragen — mit 44, 17, 33 und 26 echten
Werkzeugaufrufen und **keinem einzigen unlesbaren oder leeren Zug**.
qwen3.5:9b schaffte als erstes Modell überhaupt den TikTok-9:16-Entwurf.

### Warum die Zahlen steigen — und das ehrlich dasteht

Die ersten Nächte fielen viele Aufgaben nicht am Modell, sondern an Qwirbel
selbst: abgebrochene Modell-Ströme, Leer-Antworten im Denk-Kanal, ein
Blocker, der Aufgaben in Endlosschleifen schickte, zu wenig Sandbox-Speicher
für 1080p-ffmpeg, Blender-Socket-Namen aus Blender-2.x-Trainingsdaten.
**25 solcher „Fallen“ wurden bis zum 03.11. gefunden, repariert, mit Tests
gesichert und ausgeliefert** (v3.1.5 bis v3.2.1). Was bleibt, ist
Modell-Schwäche — und die sieht man dann ungeschönt. Die Messreihe läuft
weiter; dieser Bericht wird mitgezogen.

---

## Schnelltests (Oktober 2026, 1–4 Aufgaben je Lauf)

| Modell (Ollama) | Beste Quote | Bemerkung |
|---|---|---|
| Ornith-1.5-35B-A3B IQ4_XS | 3/3 | 1.144 s — sicher |
| gemma-4-26B-A4B UD-Q3_K_XL | 3/3 | 430 s — flottester 3/3-Lauf |
| gemma-4-26B-A4B UD-Q2_K_XL | 3/4 | scheiterte am Hasen-Nachbessern |
| Qwen3-30B-A3B-2507 UD-Q3_K_XL | 2/3 | |
| gemma-4-E4B Q4_K_M | 2/3 | |
| Qwen3.5-9B Q4_K_M | 1/1 | |
| GLM-4.7-Flash UD-Q3_K_XL | 1/4 | |
| granite-4.0-h-small UD-IQ3_XXS | 1/4 | |
| Qwen3.8-27B UD-Q2_K_XL | 1/4 | |

Insgesamt 23 Modelle gemessen; die vollständige Tabelle aller 87 Läufe
wächst im Entwicklungs-Repo mit.

---

## Was wir daraus empfehlen

- **Arbeitspferd bis ~35 B Parameter:** Ornith-1.5-35B-A3B (IQ4_XS) oder
  gemma-4-26B-A4B (Q3) — beide lösten jeden Schnelltest.
- **Unter Volllast:** bonsai-2:27b ist bisher das einzige Modell, das in der
  25-Aufgaben-Dauerprobe mehrfach 4 Aufgaben sauber löste (Video, Bild,
  GIF, Verständnis).
- **Vorsicht bei Q2-Quantisierungen großer Modelle:** Qwen3.8-27B Q2
  rechnet fachlich daneben (Mehrwertsteuer 119 statt 107).
- Kleine Modelle (unter ~10 B) sind erst seit den Fallen-Fixes fair
  messbar — ihre Quoten der ersten Nächte sagen mehr über die alte
  Umgebung aus als über das Modell.

---

*Alle Zahlen stammen aus Qwirbels eingebauter Arbeitsprobe (87 Läufe bis
03.11.2026). Kein Lauf wurde nachträglich schöngerechnet; schlechte Tage
stehen mit drin.*
