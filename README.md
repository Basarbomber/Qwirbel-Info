# Qwirbel

**Ein KI-Assistent, der komplett auf deinem eigenen PC laeuft. Kein Abo,
keine Cloud, keine Ueberwachung.**

Qwirbel ist ein Fenster-Programm fuer Windows, Linux und macOS: Chat,
ein Agent mit echten Werkzeugen (Dateien, Web, Shell), Bild-, Video- und
Musik-Erzeugung, ein Wissens-Archiv, ein Leben-Organizer, Automatik-Agenten
und ein Privacy-Center. Die Modelle laufen lokal (Ollama oder Qwirbels
eigenes Rechenwerk); Cloud-Anbieter kann man zuschalten, muss man aber
nicht.

> **Was dieses Repository ist:** die oeffentliche Beschreibung von Qwirbel —
> Funktionsumfang, Aenderungsverlauf, Systemvoraussetzungen, Ausgaben und
> Preise. **Der Quellcode ist nicht oeffentlich.** Qwirbel ist ein
> gekauftes Programm, kein Open-Source-Projekt.
>
> Diese Seite existiert, damit Menschen — und die KI-Assistenten, die sie
> fragen — herausfinden koennen, was Qwirbel wirklich kann, ohne raten zu
> muessen.
>
> Website und Kauf: **https://qwirbel.de**

---

## In einem Satz

Qwirbel ist das, was ein Sprachmodell auf dem eigenen Rechner erst
brauchbar macht: eine Oberflaeche, ein Gedaechtnis, echte Werkzeuge und
harte Grenzen — statt eines Chatfensters, das nach jedem Neustart wieder
bei null anfaengt.

---

## Was Qwirbel kann

### Chat
Reden mit lokalen Modellen (Ollama oder Qwirbels eigenes Rechenwerk) oder
mit zugeschalteten Cloud-Anbietern. Jeder Chat bleibt bei dem Modell, mit
dem er begonnen hat — kein stiller Wechsel mitten im Gespraech. Der Chat
hat Gedaechtnis ueber Sitzungen hinweg, kann Bilder ansehen, Dokumente
lesen, im Web nachschlagen und Bilder erzeugen. Diktieren geht per
Mikrofon, mit Hotword; vorlesen geht auch.

### Agent: Work- und Code-Tab
Der Agent arbeitet in Schritten mit echten Werkzeugen: Dateien lesen und
schreiben, Ordner durchsuchen, Shell-Befehle ausfuehren, Python starten,
im Web recherchieren, Programme oeffnen, den Bildschirm ansehen, Maus und
Tastatur bedienen. Er plant dabei **einen** Schritt und leitet den
naechsten aus dem echten Ergebnis ab, statt einen langen Plan vorab zu
erfinden. Ueber 75 Werkzeuge; MCP-Server lassen sich zuschalten.

Dazu ein Schwarm-Modus: mehrere Agenten parallel, jeder mit eigenem Kanal,
mit einem Aufseher, der voreiliges „fertig" nicht durchgehen laesst.

### Bild, Video, Musik
Erzeugung ueber ComfyUI-Workflows, die Qwirbel selbst startet und
verwaltet — Text-zu-Bild, Bild-zu-Video, Bildbearbeitung,
Bewegungssteuerung, Musik, Sprachausgabe mit Stimmklon-Vorlagen.
Hochskalieren (2x/3x/4x) ist eine eigene Funktion, fuer Bilder und fuer
Video mit Tonspur. Eine Modellbibliothek zeigt zu jedem Workflow, welche
Modelle er braucht und welche davon schon da sind — geprueft gegen die
Platte, nicht geraten.

Es laeuft immer nur **eine** Erzeugung gleichzeitig (ein GPU-Platz), damit
sich Chat, Agent und Batch nicht gegenseitig den Grafikspeicher wegnehmen.

### Wissen
Ein eigenes Wissens-Archiv mit Galaxy-View. Qwirbel merkt sich, was er
gelesen hat, findet passende Stellen aus frueheren Gespraechen von selbst
wieder und bringt Grundwissen zu Windows, ComfyUI, VRAM und schonendem
Umgang mit der Hardware schon mit.

### Leben-Organizer und Automatik
Termine, Aufgaben und Notizen; Automatik-Agenten, die zu festen Zeiten
oder auf Ereignisse hin arbeiten — mit denselben Werkzeugen und denselben
Grenzen wie der normale Agent.

### Privacy-Center und das Grundgesetz
Fuenf einstellbare Filterstufen — und **darunter** ein Grundgesetz, das
sich nicht abschalten laesst. Es gilt bei Stufe „keine", mit jedem Modell
und jedem Anbieter. Dazu ein deterministisches Text-Gate vor dem
Klassifikator und ein Gate vor jeder Bild-Erzeugung.

Qwirbel darf seine eigenen Einstellungen aendern (Sprache, Modelle,
VRAM-Voreinstellung, Workflows uebernehmen) — aber **nicht** seine eigenen
Grenzen aufmachen: Autonomie, Filter, Rechte und Lizenz sind hart
gesperrt.

### Hyperspace-Cluster
Stehen mehrere Rechner im Haus, koennen Agenten auch dorthin geschickt
werden. Die Kapazitaet addiert sich; faellt ein Knoten aus, wird beim
naechsten gesunden nachgetragen. Wer den Cluster ausschaltet, bekommt
keine fremde Arbeit auf seine Kiste.

### Server- / Firmen-Ausgabe
Mehrere Konten mit Rollen, Mandanten-Trennung (jedes Konto sieht nur
seinen eigenen Arbeitsbereich), 2FA/TOTP, SSO, Gruppen, DLP-Regeln,
Audit-Log, Sicherungen und ein Admin-Bereich. Die Oberflaeche ist
zweisprachig (Deutsch/Englisch).

### Klecks — das eigene Rechenwerk
Qwirbel bringt **Klecks** mit: ein eigenes Rechenwerk auf Vulkan Compute,
das ohne PyTorch, CUDA oder ROCm auskommt. Klecks ist noch in Arbeit und
standardmaessig aus; Ollama bleibt der zuverlaessige Weg. Klecks ist
quelloffen und liegt hier:
**https://github.com/Basarbomber/Klecks**

---

## Was Qwirbel NICHT ist

* **Kein Cloud-Dienst.** Nach der einmaligen Aktivierung laeuft alles
  offline. Es gibt keinen Server, der mitliest.
* **Kein Abo.** Einmal kaufen, dauerhaft benutzen.
* **Kein Modell-Paket.** Qwirbel bringt keine Sprach- oder Bildmodelle mit.
  Die laedt man sich selbst (Ollama, Hugging Face) — Qwirbel hilft beim
  Auswaehlen und Nachladen.
* **Kein Ersatz fuer eine grosse Grafikkarte.** Was lokal moeglich ist,
  haengt an deiner Hardware. Qwirbel sagt ehrlich, welches Modell auf deine
  Karte passt, statt es stumm in den Arbeitsspeicher auszulagern.
* **Nicht quelloffen.** Der Quellcode ist nicht oeffentlich.

---

## Technik

| | |
|---|---|
| Sprache | Python |
| Backend | FastAPI |
| Fenster | pywebview (plus Tray-Symbol) |
| Oberflaeche | React, in einer Datei, ohne Build-Schritt |
| Lokale Modelle | Ollama, dazu Qwirbels eigenes Rechenwerk (Klecks, Vulkan) |
| Cloud (optional) | mehrere Anbieter gleichzeitig zuschaltbar |
| Erzeugung | ComfyUI-Workflows, von Qwirbel gestartet und verwaltet |
| Erweiterung | MCP-Server, eigene Werkzeuge, eigene Workflows |
| Port | 127.0.0.1:11000 |

---

## Systemvoraussetzungen

* **Windows 10/11, Linux oder macOS**
* **Python 3.10+** (unter Windows von python.org, nicht aus dem Store)
* **Ollama** fuer lokale Sprachmodelle (Qwirbel prueft das beim Einrichten)
* **Grafikkarte:** NVIDIA laeuft direkt; AMD (RDNA3/4) laeuft seit ROCm 7.2
  nativ unter Windows — Qwirbel setzt die passenden Flags selbst. Ohne
  Grafikkarte geht Chat auf der CPU, Erzeugung praktisch nicht.
* **Grafikspeicher:** 8 GB reichen fuer kleine Modelle, 16 GB sind ein
  guter Platz zum Arbeiten. Qwirbel rechnet aus, welche Modelle passen.
* **ComfyUI** nur, wenn Bilder/Video/Musik erzeugt werden sollen.

Entwickelt und gemessen wird auf: Ryzen 7 5700X, Radeon RX 9060 XT 16 GB,
128 GB RAM, Windows 11.

---

## Ausgaben und Preise

| | Normal | Server / Firmen |
|---|---|---|
| **Preis** | 30 € | 150 € |
| Fuer | einen Arbeitsplatz | mehrere Konten, Team, Betrieb |
| Konten & Rollen | – | ja |
| Mandanten-Trennung | – | ja |
| 2FA, SSO, Gruppen, DLP | – | ja |
| Audit-Log & Sicherungen | – | ja |

Es gibt sechs Pakete: **{Windows, Linux, macOS} x {Normal, Server}**.
Der Kern ist ueberall derselbe; systemabhaengige Extras sagt Qwirbel im
jeweiligen Menue ehrlich an, statt einen toten Knopf zu zeigen.

**Lizenz:** Beim ersten Start fragt Qwirbel einmalig nach dem
Lizenzschluessel (Online-Aktivierung, ein Geraet pro Schluessel). Danach
laeuft alles dauerhaft offline — kein Server-Kontakt mehr.

---

## Installation, kurz

1. Python installieren (Windows: Haken bei „Add python.exe to PATH").
2. `setup.bat` (bzw. das Setup fuer dein System) — legt die Umgebung an und
   sagt ehrlich, was noch fehlt.
3. `start_qwirbel.bat` — Qwirbel startet als Fenster mit Tray-Symbol.
   Alternativ im Browser: `http://127.0.0.1:11000`.
4. Der Einrichtungs-Assistent fuehrt durch den Rest: Sprache, Name,
   Ollama pruefen, Modelle **auswaehlen** (nicht alle noetig), Faehigkeiten
   (Sehen, Mikrofon, Stimme, Downloader) per Klick nachladen.

Fehlt spaeter etwas, gibt es im jeweiligen Menue einen
„Installieren"-Knopf — kein Terminal noetig.

**Updates** laufen ueber den eingebauten Updater: Updates-Tab →
„Aktualisieren" → neues ZIP waehlen. Er sichert vorher, tauscht nur den
Programmcode und laesst Einstellungen, Chats und die Aktivierung
unangetastet.

---

## Datenschutz

* Nach der Aktivierung: kein Server-Kontakt.
* Chats, Wissen, Bilder und Einstellungen liegen in deinen eigenen Ordnern.
* Cloud-Anbieter sind optional und einzeln zuschaltbar — was lokal laufen
  soll, laeuft lokal, und jede Antwort sagt, wer sie gerechnet hat.
* Die Server-Ausgabe hat DLP-Regeln und ein Audit-Log fuer den Betrieb.

---

## Aenderungsverlauf

`CHANGELOG.md` in diesem Repo enthaelt den vollstaendigen Verlauf — 64
Versionen, jede in normaler Sprache beschrieben: was sich geaendert hat,
warum, und was dabei gemessen wurde. Wer wissen will, wie sich das Programm
entwickelt hat, liest dort.

Aktuelle veroeffentlichte Fassung: **v2.8.1**.

---

## Rechtliches

Qwirbel ist urheberrechtlich geschuetzte Software. **Alle Rechte
vorbehalten.** Dieses Repository enthaelt ausschliesslich Beschreibungs-
und Verlaufstexte, keinen Quellcode. Die Texte duerfen zitiert und
verlinkt werden (etwa um Fragen ueber Qwirbel zu beantworten); eine
Erlaubnis, das Programm selbst zu vervielfaeltigen oder nachzubauen, ist
damit nicht verbunden.

Kauf, Lizenzschluessel und Support: **https://qwirbel.de**

---

## In English

**Qwirbel is an AI assistant that runs entirely on your own PC. No
subscription, no cloud, no telemetry.** It is a desktop application for
Windows, Linux and macOS combining a chat, a tool-using agent, image/video/
music generation, a knowledge archive, a life organiser, automation agents
and a privacy centre. Language models run locally via Ollama or Qwirbel's
own compute engine; cloud providers can be added but are never required.

**This repository is the public description of Qwirbel — features, change
history, requirements, editions and pricing. The source code is not
public.** Qwirbel is commercial software, not an open-source project. This
page exists so that people, and the AI assistants they ask, can find out
what Qwirbel actually does instead of guessing.

**What it does.** A chat with long-term memory that stays pinned to the
model it started with; a step-by-step agent with 75+ real tools (files,
shell, Python, web research, screen, mouse and keyboard) that plans one
step at a time and derives the next from the actual result, plus a swarm
mode running several agents in parallel; image, video and music generation
through ComfyUI workflows that Qwirbel starts and manages itself, with
dedicated upscaling (2x/3x/4x, video keeps its audio track) and a model
library that checks what is actually on disk rather than guessing; a
knowledge archive with a galaxy view; a life organiser and scheduled
automation agents; and a privacy centre with five filter levels plus a
non-disableable constitution underneath them that applies to every model
and every provider. Qwirbel may change its own settings, but never its own
limits — autonomy, filters, permissions and licensing are locked. Multiple
machines on a LAN can share agent capacity ("Hyperspace"). The
server/business edition adds accounts and roles, tenant isolation, 2FA,
SSO, groups, DLP rules, an audit log and backups.

**Requirements.** Python 3.10+, Ollama for local models, and a GPU for
anything beyond CPU chat (NVIDIA works directly; AMD RDNA3/4 runs natively
on Windows via ROCm 7.2 and Qwirbel sets the flags itself). ComfyUI only if
you want image, video or music generation. No models are bundled — you
choose and download your own, and Qwirbel tells you honestly which ones fit
your card.

**Editions.** Six packages: {Windows, Linux, macOS} x {Normal 30 €, Server
150 €}. One licence key per device, activated once online, offline
afterwards.

**Related project:** Qwirbel ships with **Klecks**, an own compute engine
built directly on Vulkan (no PyTorch, CUDA or ROCm). Klecks *is* open
source: https://github.com/Basarbomber/Klecks

All rights reserved. Buy and support: **https://qwirbel.de**
