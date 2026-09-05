## v2.9.16 - Was im Paket nichts zu suchen hat, und der Ordner, der nie aufgeraeumt wurde

### Kassensturz im Paket

**Im Paket lagen Dateien, die niemanden ausser der Werkstatt etwas
angehen.** Nachgezaehlt am Windows-Paket: 782 Dateien, darunter sechs
interne Berichte (Pruefungen, Roadmap, Funktionsstand), Oberflaechen-
Entwuerfe und eine 1,5-MB-Funktionsliste als Tabelle. Dazu lagen Docker
und Helm samt Firmen-Einrichter auch in der EINZELPLATZ-Ausgabe - fuer
jemanden, der Qwirbel auf seinem eigenen Rechner benutzt, sind das
einundzwanzig Dateien Rauschen und eine Einladung, den falschen Starter
zu druecken.

**Und je System das falsche Werkzeug.** Das mitgelieferte Klecks brachte
seine Entwickler-Skripte mit: im Linux-Paket lagen zwanzig .bat-Dateien -
keine davon dort ausfuehrbar.

Jetzt sind es 744 statt 782 Dateien; die Server-Ausgabe behaelt Docker und
Helm, die Einzelplatz-Ausgabe nicht.

**Und der Filter ist eine Regel, keine Namensliste.** Die alte Liste
zaehlte einzelne Dateien auf - deshalb fuhren die Berichte vom 3.
September mit: beim letzten Nachtragen gab es sie noch nicht. Jetzt gilt
"Berichte im Hauptordner gehoeren der Werkstatt", und das altert nicht
mit.

### Der Sicherungsordner wuchs ohne Grenze

**Bei jedem Update legt Qwirbel drei Sicherungen an** - Daten, Programm-
code und einen kompletten Stand. Die ersten beiden werden seit jeher
aufgeraeumt (die letzten sieben bleiben). Der komplette Stand nicht: er
wiegt rund 700 MB und kam bei jedem Update dazu. Fuer immer.

Gemessen an einer gewachsenen Installation: **37 Voll-Sicherungen, 25
Gigabyte** in einem Ordner, von dem niemand wusste. Ab jetzt bleiben die
fuenf neuesten - das sind gut zwei Wochen Sicherheit und dreieinhalb
Gigabyte statt fuenfundzwanzig.

**Aufraeumen gehoert zum Schreiben.** Wer eine Datei anlegt, die bei jedem
Lauf wiederkommt, muss auch sagen, wie viele davon bleiben - sonst merkt
es niemand, bis die Platte voll ist.

## v2.9.15 - Die Installation wartete auf eine Taste, die niemand druecken konnte

### Zwei Stunden bei einer Sekunde Rechenzeit

**Der Setup-Test in einem leeren Ordner hat einen Fehler gefunden, der
die Installation beim Kunden fuer immer anhalten konnte** - und zwar
NACHDEM alles fertig war.

Gemessen: das Paket war entpackt, die Python-Umgebung stand, 277 Pakete
waren installiert - Kern, Diktat, Stimme, Hotword, Bildschirm-Sehen,
Downloader, alles. Und danach passierte nichts mehr. Der letzte Prozess
stand knapp zwei Stunden lang bei einer Sekunde Rechenzeit an der
letzten Zeile des Einrichtungs-Skripts:

    [Enter] zum Schliessen ...

Diese Zeile ist fuer den Doppelklick gedacht: sie haelt das Fenster
offen, damit man die Meldungen noch lesen kann. Wird das Setup aber vom
Installationsprogramm gestartet, gibt es kein Fenster und keine Tastatur
- und die Frage bleibt unbeantwortet. Der Nutzer saehe „Installation
laeuft ..." und wuerde ewig warten, obwohl in Wahrheit schon alles
fertig installiert war. Dasselbe galt fuer zwei Wartezeilen im
Fehlerfall eine Stufe hoeher.

**Jetzt wird vorher gefragt, ob ueberhaupt jemand davorsitzt.** Haengt
eine echte Konsole dran (Doppelklick), bleibt das Fenster offen wie
bisher. Kommt der Aufruf aus dem Installationsprogramm, laeuft es
durch.

### Und zwei Dinge, die beim selben Test aufgefallen sind

**Das Einrichtungs-Skript wird jetzt mit vollem Pfad aufgerufen.** Es
wurde bisher nur mit seinem Namen gestartet - das setzt voraus, dass
Windows im aktuellen Ordner sucht. Eine gaengige Haertungs-Einstellung
in Firmen schaltet genau das ab; dann waere die Datei nicht gefunden
worden, obwohl sie danebenliegt, und die Installation haette „fertig"
gemeldet, ohne eine Python-Umgebung angelegt zu haben.

**Und wenn sich das Setup-Fenster gar nicht oeffnen laesst, kommt eine
Meldung.** Bisher fiel das Setup in diesem Fall auf einen Textmodus
zurueck, den es in einem Fenster-Programm nicht gibt - der Doppelklick
war ein lautloses Nichts. Jetzt sagt ein Meldefenster, was los ist und
wie es trotzdem geht.

### Bibliotheken: „Modell hinzufuegen" mit eigener Recherche

**Unter der Modellbibliothek und der Generationsbibliothek steht jetzt
ein Feld, in das du schreibst, was dir fehlt.** Qwirbel sucht dazu ein
passendes Modell; nennst du eine Adresse, liest er die Seite mit. Was
dabei herauskommt, ist ein Vorschlag: Repo, Name, Rolle, Ordner - du
siehst ihn, kannst jedes Feld aendern, und erst dein Klick nimmt ihn
auf.

**Dazwischen schlaegt Qwirbel selbst nach.** Ein Sprachmodell nennt
gelegentlich ein Repo, das es gar nicht gibt - plausibel geschrieben und
trotzdem erfunden. Deshalb wird vor dem Aufnehmen bei Hugging Face
geprueft, ob es das Repo wirklich gibt und ob die versprochenen Dateien
darin liegen. Steht dort nichts, wird nichts aufgenommen.

**Die Regel „nur aus geprueften Quellen laden" bleibt.** Sie wird nicht
aufgeweicht, sondern waechst um genau den einen Eintrag, den du
bestaetigt hast - und den du unten in derselben Liste auch wieder
entfernen kannst.

## v2.9.14 - Ein Aussetzer legt nicht mehr die ganze Aufgabe still

Diese Fassung kommt aus einem echten Lauf: ein Modell ueber die
Programmierschnittstelle, im Code-Bereich, mit Roblox Studio ueber MCP.
Vier Werkzeug-Aufrufe liefen sauber - Instanzen auflisten, Zustand
abfragen, den laufenden Test stoppen, Skripte durchsuchen. Danach ging
Studio verloren.

### Die Sperre ging nie wieder auf

**Wenn das Zielprogramm nicht mehr an der Bruecke haengt, setzt Qwirbel
eine Sperre** - bestehende Dateien dieses Ziels sind dann tabu, und der
Nutzer bekommt einen Satz, was er einschalten muss. Das ist richtig so:
blind etwas umschreiben ist schlimmer als anzuhalten.

**Nur ging die Sperre nie wieder auf.** Sie wurde an genau einer Stelle
entfernt - wenn das Modell einen NEUEN Server dazuholt. Kam das Programm
von selbst zurueck, blieb sie stehen, und die Aufgabe war tot: im
gemessenen Lauf drei Minuten lang dieselbe Notiz, kein einziger
Werkzeug-Aufruf mehr. Jetzt hebt ein gelungener Aufruf an denselben
Server die Sperre auf - der Beleg ist der Aufruf selbst, kein
Versprechen, und ein anderer Server zaehlt dafuer nicht.

### Ein kurzer Aussetzer bekommt einen zweiten Anlauf

**Beim Umschalten zwischen Test und Bearbeiten meldet sich Roblox Studio
kurz ab.** Der erste Aufruf danach lief ins Leere - und weil daraufhin
sofort die Sperre fiel, sah eine Sekunde Unterbrechung aus wie ein
geschlossenes Programm.

**Die Bruecke kann warten** - beim Start tut sie das seit einer Weile,
bis zu zwanzig Sekunden. Jetzt bekommt auch ein bestehender Kanal diese
Geduld: Bruecke zu, Bruecke auf, Aufruf noch einmal. Ist das Programm
wirklich weg, kommt derselbe Fehler zurueck und die Sperre greift wie
bisher - nur belegt statt vermutet.

## v2.9.13 - Bilder kommen an, und MCP-Werkzeuge lassen sich benutzen

### „Liegt nicht mehr auf dem Rechner" - und lag die ganze Zeit da

**Ein eingefuegtes Bild wurde angezeigt und kurz darauf durch einen
Platzhalter ersetzt, der behauptete, die Datei sei weg.** Sie war es nie.
Ein Bild-Tag laedt der Browser selbst und kann dabei keinen
Anmelde-Header mitschicken; dafuer gibt es eine kurze Liste von Adressen,
die den Schluessel auch aus der Adresszeile annehmen duerfen. Die Adresse
des Bild-Registers - seit der letzten Fassung der Weg fuer JEDES Chatbild -
stand nicht darin. Wer ein Passwort gesetzt hatte, bekam damit auf jedes
Bild eine Absage. Das betraf auch die Bilder an Ergebnissen in Code und
Work.

**Und der Platzhalter hat geraten.** Er nannte jeden Ladefehler „liegt
nicht mehr auf dem Rechner" - auch eine abgelaufene Anmeldung, auch eine
abgerissene Verbindung. Jetzt wird erst beim Server nachgefragt, und zwar
auf demselben Weg, der gescheitert ist. Danach steht dort, was wirklich
los ist: Anmeldung, unbekannte Datei, oder tatsaechlich geloescht - dann
mit Namen und Datum. Dazu ein zweiter Weg zur selben Datei, bevor
ueberhaupt geklagt wird, und ein Knopf zum Nochmal-Versuchen.

### MCP: das Modell sah nicht, was die Werkzeuge wirklich wollen

**Werkzeuge, die ein fremdes Programm steuern, verlangen genaue
Argumente - und Qwirbel hat die entscheidende Haelfte davon weggeworfen.**
Zwei Stellen:

Erstens ein Deckel: nur die ersten sechs Felder eines Werkzeugs kamen in
die Beschreibung, danach fiel alles weg - auch PFLICHTfelder. Ein Aufruf,
der dem Beispiel folgte, war unvollstaendig.

Zweitens die erlaubten Werte. Steht im Werkzeug „nimm eines von Edit,
Client, Server", stand in der Beschreibung nur „Text". Beim Schreiben von
Skripten in Roblox Studio ist genau ein Wert erlaubt - das Modell konnte
es nicht wissen, hat geraten, ist abgeprallt und hat danach nur noch
gelesen statt gearbeitet.

**Beides steht jetzt da.** Pflichtfelder fallen nie mehr heraus, und wo
das Werkzeug erlaubte Werte kennt, stehen sie im Beispiel. Gemessen an
einer Installation mit neun Servern und 97 Werkzeugen kostet das zwei
Prozent mehr Text.

### Nicht stundenlang derselbe Fehler

**Scheitert ein Aufruf an den Argumenten, sagt die Antwort jetzt, woran.**
Welches Pflichtfeld fehlt, welcher Wert nicht erlaubt ist und welcher es
waere - aus der Beschreibung des Werkzeugs selbst, nicht geraten. Das
passiert nur im Fehlerfall; ein Aufruf, der laeuft, bekommt keinen
Kommentar.

**Und derselbe Fehlschlag wird gezaehlt.** Wird ein Werkzeug ein zweites
Mal mit exakt denselben Argumenten gerufen und scheitert wieder gleich,
steht das in der Antwort. Geaenderte Argumente sind Arbeit und bekommen
keinen Vorwurf. Gesperrt wird dabei nichts - die einzige Grenze fuer
MCP-Werkzeuge bleibt die Modellgroesse in den Einstellungen.

## v2.9.12 - Standarddienste: wer macht was, und wie kommt einer dazu

### Ein Tab, der sagt, wer der Standard ist

**Bisher stand die Frage „wer rechnet eigentlich?" an vier Stellen und
nirgends ganz.** Der Motor fuer Sprachmodelle steckte in einer Einstellung
namens `llm_engine`, die Wahl fuer Bilder in zwei anderen Werten, und wer
sonst noch bereitsteht, sah man nur im Autostart-Tab. Unter Einstellungen →
Standarddienste steht das jetzt zusammen: je Aufgabe der Standard, daneben
das, was sonst mitlaeuft, und ein Punkt, der zeigt, was gerade wirklich
antwortet.

**Umgestellt wird dabei nichts Neues.** Wer hier den Standard aendert,
schreibt in genau die Werte, die es vorher schon gab. Ein zweiter Schalter
daneben waere beim naechsten Update auseinandergelaufen.

**Und Klecks steht jetzt in beiden Rollen.** Er rechnet Sprache UND Bilder -
in der ersten Fassung dieses Tabs tauchte er unter Bildern gar nicht auf,
obwohl die Motorwahl ihn seit dem 26.08. ausdruecklich anbietet.

### Der Plus-Knopf: eine Engine dazunehmen, die du gefunden hast

**Neben jeder Aufgabe steht ein Plus.** Du sagst, was du gefunden hast -
einen Namen oder einen Link -, und ein Modell sieht nach und schlaegt einen
Steckbrief vor: Name, Adresse, Pruefweg, wofuer der Dienst gut ist. Nennst du
eine Adresse, wird deren Text wirklich geholt und dem Modell vorgelegt. Du
siehst den Vorschlag, kannst jedes Feld aendern, und erst dein Klick nimmt
ihn auf.

**Spricht der Dienst die OpenAI-API - und das tun die meisten -, ist er
danach ein vollwertiger Anbieter.** Er steht im Modell-Menue und kann alles,
was ein Anbieter kann: Chat, Aufgaben, Planung, Werkzeuge. Denselben Weg
geht Colibri seit dem 24.08.; es wurde also kein zweiter LLM-Pfad gebaut.

### Wo die Grenze liegt, und warum sie dort liegt

**Qwirbel laedt dabei kein Programm herunter und fuehrt nichts aus, was ein
Modell geschrieben hat.** Hinzugefuegt wird eine Beschreibung, keine
Installation. Das ist keine Bequemlichkeitsgrenze: „kein ferngeladener Code"
ist eine der Regeln, die in diesem Programm nicht abschaltbar sind, und ein
Plus, das im Hintergrund ein fremdes Binary zieht und startet, waere genau
der Weg, den der Web-Filter seit Wochen zumauert. Der Vorschlag sagt dir
stattdessen, wie du die Engine installierst - und dieser Satz steht sichtbar
in der Karte, nicht im Kleingedruckten.

**Selbst hinzugefuegte Dienste startet Qwirbel nicht.** Sie werden benutzt,
sobald sie laufen. Auch das steht dort, statt einen Schalter zu zeigen, der
nichts tut.

**Drei Stufen halten die Regel, nicht eine.** Das Modell wird angewiesen,
keinen Befehl zu liefern; die Feldliste uebernimmt ohnehin nur bekannte
Schluessel; und wenn trotzdem einer mitkam, steht das als Warnung da. Der
letzte Punkt kam erst durch den eigenen Test dazu - bis dahin wurde ein
untergeschobener Befehl zwar weggeworfen, aber stillschweigend. Weggeworfen
und verschwiegen ist fast so schlecht wie gar nicht gemerkt.

### Kleinigkeiten am Rande

**Sicherungskopien fuhren im Paket mit.** Acht Dateien aus dem
Klecks-Quellstand (885 KB toter Quelltext) lagen in jedem der sechs Pakete;
der Filter dafuer traf nur eine Schreibweise statt die Sache. Beide Seiten
benutzen jetzt dieselbe Liste.

**Eine Fehlermeldung, die niemand sah.** Scheiterte die Engine-Recherche -
etwa weil ein API-Guthaben leer ist -, meldete das Backend das sauber, und
die Oberflaeche zeigte gar nichts: der Text landete in einer Karte weit
unterhalb des Blickfelds. Er steht jetzt neben dem Knopf, den man gedrueckt
hat.

## v2.9.11 - Wo liegen eigentlich meine Modelle? Und wie schiebe ich sie um?

### Die groesste Frage stand ueberhaupt nicht im Programm

**Unter Einstellungen → Dateien & Speicher gab es eine Landkarte - aber nur
von dem, was im Programmordner liegt.** Der mit Abstand groesste Posten
stand nirgends: Ollamas Modell-Speicher, weil der in einer
Umgebungsvariablen wohnt. Genauso wenig ComfyUIs Checkpoints, Colibris
Experten-Dateien oder Kimis Zwischenspeicher. Wer wissen wollte, warum die
Platte voll ist, fand die Antwort im Windows-Explorer statt in Qwirbel. Und
aendern liess sich gar nichts.

**Jetzt steht dort jeder Ordner, den Qwirbel anlegt oder benutzt** - mit
seinem Laufwerk, dem freien Platz darauf und der gemessenen Groesse. Daneben
steht, wer den Ordner liest und ob er eingestellt oder nur die Vorgabe ist.
Eine Zeile weiter unten sagt eine Ampel, ob gerade ein Programm darauf
zugreift; das wird nachgesehen, nicht geraten.

### Umziehen mit einer Frage vorher, nicht einer Entschuldigung hinterher

**Jeder dieser Ordner laesst sich jetzt aendern - und Qwirbel fragt erst,
was mit den Dateien passieren soll.** Drei Wege stehen nebeneinander:
mitnehmen und am alten Ort loeschen, mitnehmen und den alten Ort als
Sicherung behalten, oder nur den Ordner umstellen und nichts anfassen. Die
Partition waehlst du per Klick aus der Liste deiner Laufwerke.

**Vorher wird gerechnet, nicht gehofft.** Qwirbel misst den Ordner
vollstaendig, vergleicht mit dem freien Platz am Ziel und sperrt, was
schiefgehen wuerde - ein Ziel im Quellordner, derselbe Ordner, ein Pfad ohne
Laufwerk, zu wenig Platz. Verschoben wird immer in dieser Reihenfolge:
kopieren, jede einzelne Datei am Ziel gegen das Original pruefen, und erst
danach den alten Ort raeumen. Bricht etwas ab, kostet das Plattenplatz -
aber nie Daten. Gleichnamige Dateien am Ziel werden nicht ueberschrieben;
sie bleiben stehen, die Quelldatei auch, und beides steht danach im Bericht.

### Ein Fund, der Ollama lautlos modell-los gemacht haette

**Ordner koennen ineinander liegen.** Auf dem Entwicklungsrechner zeigte
`models_dir` auf `E:\Qwirbel models` und Ollamas Speicher auf `E:\Qwirbel
models\ollama` - der eine steckt im anderen. Wer den aeusseren umgezogen
haette, haette Ollamas Modelle mitgenommen, waehrend die Einstellung von
Ollama weiter auf den alten, jetzt leeren Ordner zeigte. Ohne Fehlermeldung,
einfach keine Modelle mehr. Qwirbel erkennt solche Verschachtelungen jetzt,
sagt sie im Menue an und stellt den inneren Ordner beim Umzug mit um.

### Das Setup hat etwas versprochen, was es nie getan hat

**Schritt 3 der Installation sagt woertlich: "Setzt OLLAMA_MODELS und traegt
den Pfad in Qwirbels Einstellungen ein."** Der zweite Halbsatz stimmte
nicht - eingetragen wurde nie etwas, mit der Begruendung, das lese ohnehin
niemand. Es liest aber jemand: genau dieser Wert entscheidet, wo Qwirbel
nach deinen eigenen Modell-Dateien sucht. Fehlt er, sind sie unsichtbar.
Das Setup loest das Versprechen jetzt ein und sagt ausserdem dazu, was es
NICHT fragt: ComfyUI und Klecks bringen eigene Ordner mit, und die stellst
du spaeter im Programm um.

### Und noch eine Falle daneben

**Qwirbel sucht Modelle auch in dem Ordner, der neben Ollamas Speicher
liegt.** Wer im Setup einen Ordner direkt auf einer Platte waehlt - etwa
`E:\KI-Modelle` - bekam als Nachbarn das ganze Laufwerk `E:\`. Bei jedem
Modell-Scan lief Qwirbel dann einmal durch die komplette Platte. Kein
Fehler, nur zaeh. Der Nachbar ist jetzt nie mehr ein Laufwerk.

## v2.9.10 - Deine Bilder sind wieder da. Und ein Aussetzer wirft ihn nicht mehr um.

### Die Bilder waren nie weg - der Server gab sie nur nicht heraus

**Gemessen ueber 138 Chatdateien: 293 Bildverweise, 283 Dateien lagen noch
auf der Platte, und herausgegeben wurde keine einzige.** Es gab drei
verschiedene Erlaubnislisten, und in keiner standen ausgerechnet die beiden
Ordner, in die Qwirbel selbst schreibt - Bildschirmfotos und Eingefuegtes.
Dazu ein Pfad, der beim Ausliefern kaputtging, und generierte Bilder, die am
laufenden ComfyUI hingen. An keinem Bild hing eine Fehlerbehandlung, deshalb
blieb das Bruchsymbol des Browsers stehen.

**Jetzt entscheidet ein Bild-Register, nicht mehr die Ordnerliste.** Was
Qwirbel gezeigt oder erzeugt hat, bekommt eine Kennung - und die steht in
der Adresse statt eines Pfades. Zieht eine Datei um, findet er sie am Namen
wieder und merkt sich den neuen Ort. Beim Start werden alle Chats
nachgetragen, auch die archivierten, damit Unterhaltungen von vor Wochen
ihre Bilder zurueckbekommen. Fehlt eine Datei wirklich, steht dort ein
Platzhalter mit Namen und Datum statt eines kaputten Symbols. Nach dem Umbau
gemessen: 146 von 153 Dateien kommen heraus, sieben sind wirklich geloescht.

### Uebersetzung: der Regler und das Menue blieben deutsch

**Zwei Ursachen, beide unsichtbar im Programm.** Die Muehe-Tabellen wurden
beim Laden der Datei ausgewertet - da war das Woerterbuch noch nicht geholt,
und der deutsche Text fror fuer immer ein. Und acht Stellen hatten eine
eigene kleine Uebersetzung, die das Woerterbuch gar nicht kannte; deshalb
blieben der Mehr-Knopf, die Gruppen-Ueberschriften und der Hinweis unten
deutsch, obwohl alles andere polnisch war. Beides ist behoben, der Sammler
findet jetzt 2.693 statt 2.504 Texte, und eine Pruefung wacht darueber, dass
so etwas nicht wiederkommt. Wer schon eine Sprache angelegt hat, laesst sie
einmal weiteruebersetzen.

### Ein Netz-Aussetzer beendet keinen Lauf mehr

**Bisher gab es keinen einzigen Wiederholversuch.** Ein Aussetzer von einer
Sekunde hat einen Auftrag beendet, der schon vier Schritte gearbeitet hatte -
und weil im Chat deine Modellwahl gilt, stand dort nur ein Anbieter, nach dem
ersten Fehler war sofort Schluss. Jetzt wird bei Verbindungsproblemen,
Zeitueberschreitungen und ueberlasteten Anbietern bis zu dreimal versucht,
mit Pause. Bei einem falschen Schluessel oder fehlendem Guthaben natuerlich
nicht - das ist beim dritten Mal genauso falsch, und Warten wuerde nur die
Ursache verdecken. Ist schon Text bei dir angekommen, wird nichts wiederholt,
damit nichts doppelt dasteht.

### Autostart: alle Programme an einem Ort

**Settings hat einen neuen Punkt: Autostart.** Dort stehen alle Programme,
die Qwirbel selbst hochfahren kann - Ollama, Klecks, ComfyUI, Colibri und
Kimi -, jeweils mit einem Satz dazu, der Adresse und einem Schalter. Der
Punkt daneben zeigt, was gerade wirklich laeuft: nachgesehen, nicht geraten.
Die Schalter gab es zum Teil schon, sie standen nur in vier verschiedenen
Tabs; hier aendern sie genau dieselben Werte. Ollama hatte gar keinen -
Qwirbel konnte den Dienst nie selbst starten, sondern nur danach fragen. Das
kann er jetzt, und beim Schliessen beendet er nur, was er selbst gestartet
hat.

### Der Grundschutz kann nicht mehr still ausfallen

**An zwei Stellen wurde beim Bildermachen jeder Fehler des Inhaltsfilters
verschluckt.** Waere der Filter beschaedigt gewesen, haette Qwirbel weiter
Bilder erzeugt - ohne Pruefung und ohne den unabschaltbaren Grundschutz, und
niemand haette es gemerkt. Fuer ein Programm, das verkauft wird, ist das der
schlimmste Fehler ueberhaupt: der Schutz ist da und wirkt nicht. Jetzt gilt:
kein Schutz, kein Bild - mit Begruendung im Klartext.

### Eine Ablehnung haelt jetzt

**Wer abgelehnt wurde, konnte es mit einem Satz aufheben.** Der abgelehnte
Auftrag blieb als normale Nachricht im Verlauf und ging beim naechsten Zug
wieder ans Modell; ein "ich bin der Besitzer" reichte, damit es ihn doch
ausfuehrte - der Inhalt lag ja schon vor. Ab jetzt bekommt eine abgelehnte
Nachricht eine Marke: du siehst sie weiter im Verlauf, das Modell bekommt an
ihrer Stelle nur noch den Hinweis, dass hier etwas abgelehnt wurde und warum.
Dasselbe gilt fuers Zusammenfassen und fuers Lernen - sonst waere der
Wortlaut ueber Umwege zurueckgekommen. Und eine behauptete Rolle
("Ersteller", "Admin") oder ein Vorwand ("fuer einen Freund", "mach
trotzdem") aendert nichts mehr: Rechte stehen im Konto, nicht in der
Nachricht.

### Keine NSFW-Modelle, keine entsicherten Modelle

**Qwirbel richtet solche Modelle nicht ein - an allen vier Tueren, durch die
ein Modell hereinkommt.** Bei Bildmodellen ist der Grund offensichtlich. Bei
Sprachmodellen, denen die Sicherheits-Ausrichtung entfernt wurde
("uncensored", "abliterated"), ist er wichtiger: mit ihnen waere jeder
Schutz dieses Programms wirkungslos, ohne dass jemand etwas davon merkt - man
muesste ihn nicht aushebeln, man wechselt einfach das Modell. Ein Modell, das
solche Inhalte ERKENNT, bleibt selbstverstaendlich erlaubt.

### Kleinigkeiten

Der gelbe Qwirbeln-Knopf steht in beiden Leisten ganz rechts, der Pfeil nach
oben links in der Ecke vor den Kapiteln. Ein Anbieterwechsel im laufenden
Auftrag steht jetzt im Protokoll, statt lautlos zu passieren. Und die
Recherche sagt Bescheid, wenn ihr die Ethik-Leitplanke fehlt, statt still
ohne sie zu arbeiten.

## v2.9.9 - Er hoert nicht mehr still auf. Und jeder baut sich seinen Tab.

### Eigene Tabs: der Plus-Knopf links

**Unter der Tab-Leiste steht jetzt ein Plus.** Ein Klick, und du
beschreibst einen Tab, den es noch nicht gibt - das Modell, das oben im
Chip steht, baut ihn. Drei Modi, weil nicht jeder gleich viel schreiben
will: **Einfach** (ein Satz genuegt), **Erweitert** (Wie soll der Tab
heissen? Was sind seine Funktionen? Wie arbeitet er mit anderen Tabs
zusammen?) und **Vorgaben** (acht fertige Ideen zum Anklicken, danach
aenderbar - Rezepte, Lernkarten, Training, Ausgaben, Projekt, Pflanzen,
Schreiben, Reise).

**Der Bauplan wird gezeigt, bevor er in der Leiste landet.** Du siehst
Name, Icon, Zweck und jeden Baustein, kannst neu bauen lassen und legst
ihn erst auf Knopfdruck ab. Ein Tab, der ungefragt in der Leiste steht,
waere eine Zumutung.

**Ein Tab besteht aus vier Bausteinen, und alle vier tun wirklich
etwas:** ein erklaerender Absatz, ein Textfeld, dessen Inhalt bleibt,
eine Liste zum Abhaken (Punkte kommen dazu und weg), und ein Knopf, der
dein Modell mit dem Inhalt deiner Felder arbeiten laesst. Gemessen am
03.09.2026 mit GLM-5.3: aus einem Satz ueber Pflanzen entstanden sieben
Bausteine, und der Knopf "was fehlt ihr?" hat die Gieß-Routine aus der
Liste mitgelesen und die Diagnose ins Ergebnisfeld geschrieben.

**Was das Modell dabei NICHT tut: Code schreiben, der ausgefuehrt wird.**
Es liefert eine Beschreibung, die die Oberflaeche zeichnet. Erfindet es
ein Icon oder einen fuenften Bausteintyp, wird das geradegezogen statt
abgelehnt - ein Bauplan, der an einer Kleinigkeit scheitert, kostet dich
sonst einen ganzen Modell-Lauf. Und ein Knopf kann nur den Auftrag
ausfuehren, der in seinem gespeicherten Bauplan steht: ein erfundener
Knopftitel wird abgewiesen, sonst waere das ein freier Modell-Zugang an
Stufe und Tageslimit vorbei. Eigene Tabs liegen je Nutzer getrennt, wie
alles andere auch.

### Kein "Ziel erreicht" mehr, wenn die Planung abbricht

**Zweite Ursache fuer "er hoert einfach auf" - gefunden beim Durchsehen
des Agenten.** Nach jedem Schritt fragt Qwirbel das Modell: fertig, oder
was kommt jetzt? Antwortete das Modell dort nicht (abgestuerzt, Budget
erreicht, Antwort unlesbar), stand im Tab **"Ziel erreicht"** - genau
wie bei echter Fertigstellung. Der Lauf ging freundlich in die Pruefung,
und die halbe Arbeit sah aus wie eine ganze. Jetzt gibt es drei
Ausgaenge statt zwei: Schritt angehaengt, Ziel erreicht, oder
**"Planung abgebrochen: ..."** mit dem Grund im Klartext. Ein erreichtes
Token-Budget beendet den Lauf sogar ausdruecklich, statt still
weiterzurechnen.

### Uebersetzung: die Seitenleiste bleibt nicht mehr deutsch

**Falko hat auf Polnisch umgestellt, und die ganze linke Leiste blieb
deutsch.** Grund: die Tab-Namen stehen nicht als uebersetzbarer Text im
Programm, sondern in einer Tabelle - der Sammler sah sie nie, und die
Anzeige holte sie direkt von dort. Jetzt gehen Tab- und Untertab-Namen
durch dieselbe Uebersetzung wie jeder andere Text, und der Sammler liest
die Tabelle mit.

**Und "vollstaendig" war unerreichbar.** Gezaehlt wurden 2444 Texte,
uebersetzbar waren 2406: 38 Texte standen mit zwei englischen Fassungen
doppelt in der Liste, im Woerterbuch aber nur einmal. Der Knopf sagte
darum ewig "weiter uebersetzen". Jetzt zaehlt, was zaehlbar ist - je
deutschem Text einmal.

### Sprachpakete: herunterladen statt rechnen

**Wer eine Sprache anlegt, bekommt sie ab jetzt als fertiges Paket, wenn
es eines gibt.** Qwirbel schaut dort, wo auch das Update-Manifest liegt
(oder unter der Adresse, die das Manifest selbst nennt), laedt das
Woerterbuch und mischt es ein; vorhandene Uebersetzungen bleiben. Was
das Paket nicht abdeckt, rechnet das Modell wie bisher weiter - und
steht kein Paket bereit, sagt die Anzeige genau das, statt zu schweigen.
Gebaut werden die Pakete mit `scripts/sprachpakete_bauen.py` (lokales
Modell) oder `scripts/sprachpakete_teile.py` (in Teilen, mit Pruefung
auf Anzahl und Platzhalter).

### Kleinigkeiten

- **Die zwei Fenster des Baudialogs sitzen richtig.** Sie hatten nur eine
  Hoechstbreite, aber keinen Rahmen wie jeder andere Tab - dadurch klebten
  die Karten oben links am Rand und die Seite scrollte nicht. Jetzt
  derselbe Rahmen wie in Verbindung, MCP oder Backup, mit dem Abstand
  INNEN, damit die UI-Groesse ihn mitskaliert.
- **Der Plus-Knopf steht auch in der Kopfleiste.** Wer mit der fliegenden
  Kopfleiste arbeitet, hat die Seitenleiste zugeklappt und kam gar nicht
  an das Plus. Jetzt liegt es unter "Mehr", unten neben Settings.
- **Das Modell entscheidet nicht ueber das Aussehen.** Es liefert Felder,
  Listen, Knoepfe und Texte; Farbe, Abstaende und Anordnung macht die
  Oberflaeche. Die Akzentfarbe eines eigenen Tabs kommt aus einer festen
  Palette, gewaehlt nach seiner Kennung: gleiche Kennung, gleiche Farbe,
  jedes Mal. Der Auftrag an das Modell sagt das ausdruecklich, damit es
  gar nicht erst anfaengt, CSS zu schreiben.
- **Ein Absturz, der nur im echten Bild zu sehen war.** Der Zustand der
  eigenen Tabs lag zuerst in der Chat-Komponente statt in der App. Die
  Leiste zeigte den Tab, aber sein Inhalt lief in "eigenZustand is not
  defined" und damit in die Absturzseite. Kein Textprueftest findet das -
  gefunden beim Durchklicken der Web-Demo.
- **Die Web-Demo zeigt die eigenen Tabs.** Sie steht auf 2.9.9 und bringt
  einen fertig gebauten Beispiel-Tab mit (Pflanzen, sieben Bausteine, mit
  Eintraegen und einem abgehakten Punkt), dazu die acht Vorgaben im
  Baudialog. Schreibende Klicks lehnt die Demo wie ueberall ehrlich ab.
- **"Kompakt" heisst jetzt "Komprimieren"** (Falko: "Kompakt umbenennen
  zu komprimieren"). Die Karte im Verlauf heisst entsprechend
  "KOMPRIMIERT"; die Rolle in gespeicherten Chats bleibt, wie sie ist -
  ein Umbenennen dort waere ein Datenbruch ohne Gegenwert.

### Herzschlag gegen das stille Aufhoeren

**„Er hoert einfach auf“ – mitten in der Aufgabe, ohne Antwort, ohne
Fehlermeldung.** Gemessen war die Ursache der Frontend-Zeitwaechter:
zwei Minuten ohne EIN Stream-Paket gelten als tote Verbindung. So lange
brauchen RAG-Suche und langes Modell-Denken aber regelmaessig, ohne ein
einziges Paket zu schicken. Der Waechter brach ab, und fuer den Nutzer
sah es aus, als haette Qwirbel resigniert.

**Jetzt schickt das Backend in stillen Phasen alle 30 Sekunden ein
Lebenszeichen.** _mit_herzschlag() wickelt beide langen Streams (/chat
und /task/stream): solange der echte Generator nichts liefert, fliesst
ein {"event":"herzschlag"}-Paket. Es fuettert den Waechter zurueck und
bleibt sonst unsichtbar - die Oberflaeche zeigt nichts davon. Echte
Chunks und Fehler gehen unveraendert durch, der Lauf dahinter wird nie
abgebrochen. qwirbeln und komprimieren schicken ohnehin eigene
Fortschritts-Pakete und brauchten nichts.

### Internes Denken ist jetzt ein eigenes Fach

**Bisher steckte der Gedankengang in „Antworten des Modells“.** Ein
Modell, das minutenlang denkt, sah in der Faecher-Anzeige aus wie
Arbeit. Jetzt messen ollama_client und api_manager mit, wie viele
Zeichen Denken (thinking / reasoning_content) und wie viele sichtbare
Antwort flossen - die EINE completion-Zahl des Anbieters wird anteilig
auf die Faecher „denken“ (Gluehbirne) und „antwort“ verteilt, dieselbe
ehrliche Methode wie beim Prompt. Ohne Messung bleibt alles bei
„antwort“: kein Bruch, nur keine Aufteilung.

Beides wird erst nach einem Neustart von Qwirbel (window.py) aktiv -
der laufende Prozess arbeitet noch mit den alten Dateien.

## v2.9.8 - Erst sehen, dann aendern. Und wofuer die Tokens wirklich gehen.

### Roblox Studio und die Sichtpflicht

**Qwirbel hat in Roblox Studio nie wirklich hineingesehen.** Der Auftrag
"fix das Menue in meinem Spiel" endete damit, dass er Dateien umschrieb,
etwas probierte und am Ende sagte, man solle selbst nachsehen. Der Grund
war gemessen ein einziger: Qwirbel startete die Roblox-Bruecke fuer jeden
Aufruf frisch, rief sofort und schloss sie wieder. Studio haengt sich aber
erst ein paar Sekunden nach dem Start an die Bruecke - bei null Sekunden
antwortet sie "No Roblox Studio instances are connected", bei fuenf
Sekunden "Studio Mode: Edit". Der Schalter in Studio war die ganze Zeit
an. Jeder Aufruf traf also eine Bruecke, an der Studio noch nicht dran
war, und Qwirbel arbeitete nach der Regel "einmal wiederholen, sonst ohne
sie weiter" blind weiter.

**Jetzt bleibt die Bruecke zu einem Programm offen.** Beim ersten Aufruf
wartet Qwirbel, bis Studio antwortet (bis zu zwanzig Sekunden), danach
laufen alle weiteren Aufrufe ueber dieselbe Verbindung in Millisekunden.
Meldet Studio spaeter "nicht verbunden", weil es geschlossen wurde,
startet der naechste Aufruf die Bruecke frisch und wartet wieder. Gemessen
am offenen Studio: erster Aufruf 2,5 Sekunden, jeder weitere unter einer
Zehntelsekunde.

**Jetzt prueft Qwirbel vor dem ersten Zug, ob das Programm wirklich
dranhaengt.** Ein einziger billiger Aufruf an die Bruecke sagt, ob Studio
antwortet. Tut es das nicht, bekommst du sofort den einen Satz, was du
einschalten musst - in Studio den Assistant oeffnen, im Drei-Punkte-Menue
"Manage MCP Servers" waehlen und "Enable Studio as MCP server"
einschalten. Derselbe Waechter sitzt auch mitten in der Arbeit: meldet
irgendein MCP-Aufruf, dass das Zielprogramm nicht verbunden ist, gilt ab
diesem Moment die Sichtpflicht.

**Sichtpflicht heisst: was er nicht sehen kann, aendert er nicht.** Solange
Roblox Studio, Unity, Godot oder Blender nicht an ihrer Bruecke haengen,
sind bestehende Dateien dieses Ziels fuer ihn gesperrt - nicht als Bitte
im Prompt, sondern in der Ausfuehrung. Neue Dateien darf er anlegen, die
kann man wegwerfen. Sein Schlussbericht sagt dann ehrlich "blockiert:"
und nennt den Satz, statt "gebaut, schau selbst nach".

**Dabei kam ein Altfehler ans Licht.** Der Hinweis, dass ein Ziel nur
ueber die MCP-Bruecke pruefbar ist, sollte laut Kommentar "in jeden
Zug-Prompt" - stand aber im Code hinter der Arbeitsschleife. Kein einziger
Arbeitszug hat ihn je gesehen, erst die Nachbesser-Runde. Jetzt steht er
vor dem ersten Schritt, und die Suite prueft die Reihenfolge. Und weil
ein Modell im Probelauf die Sperre prompt ueber ein Python-Skript umging,
zaehlt auch Code, der eine bestehende Ziel-Datei nennt, als Umschreiben.

**Ab siebzig Milliarden Parametern holt er sich einen fehlenden Server
selbst.** Fehlt fuer ein Ziel der MCP-Server ganz, sucht ein grosses
Modell (oder jedes Cloud-Modell) ihn im Store, installiert ihn, schaltet
ihn ein und holt die Werkzeugliste in die laufende Aufgabe - in einem
Zug. Die Schwelle steht in den Einstellungen unter "MCP SELBST HOLEN AB";
darunter sagt er dir in einem Satz, welchen Server du im MCP-Tab
brauchst.

### Wofuer die Tokens gehen

**Vierzig Millionen Tokens fuer eine Menue-Aenderung - und nirgends stand,
wofuer.** Der Zaehler kannte je Chat nur die Summe. Jetzt fuehrt Qwirbel
Faecher: Dateien lesen, Dateien schreiben, Befehle ausfuehren, Hinsehen,
Web, MCP-Aufrufe, Gedaechtnis, die Grundausstattung aus Werkzeug-Doku und
System, der Auftrag selbst und die Antworten des Modells. Jeder Modell-
Zug wird nach dem Anteil seiner Prompt-Teile verteilt, der Cache-Anteil
von vorn vergeben - so, wie die Anbieter tatsaechlich cachen.

**Zu sehen ist das an zwei Stellen.** Faehrst du waehrend der Arbeit mit
der Maus ueber die Laufanzeige neben der Denkfigur, stehen dort die
Faecher dieser Aufgabe als Leisten mit Symbol. Der Kontextkreis oben
zeigt dasselbe fuer den ganzen Chat - gemessen, nicht geschaetzt. Eigene
Faecher, die sich die KI anlegt, bekommen ein eigenes Symbol aus einer
Auswahl von ueber dreissig.

**Und der Prompt ist so sortiert, dass der Cache greift.** Die grossen
Bloecke, die nur wachsen (was in diesem Chat schon passiert ist, was
gelesen wurde, der Datei-Wegweiser), stehen jetzt vor den Bloecken, die
sich jeden Schritt aendern. Vorher stand die Bilanz vorn - und der
gesamte Lese-Block dahinter war fuer jeden Anbieter ab dem zweiten
Schritt neu zu bezahlen.

### Kompakt: die KI komprimiert den Chat

**Neben Export, Loeschen und Qwirbeln gibt es jetzt Kompakt.** Ein Klick,
und das Modell fasst den bisherigen Chat zu einem Protokoll zusammen: was
fertig ist, was entschieden wurde, welche Dateien angefasst sind, was
offen ist, wo es weitergeht. Ab dieser Stelle faengt das Kontextfenster
neu an - der Kopf-Platz oben zaehlt ab da, und das Modell sieht statt des
alten Wortlauts nur noch die Zusammenfassung. Fuer dich bleibt jede
Nachricht sichtbar; die Zusammenfassung sitzt als schmale, aufklappbare
Trennlinie im Verlauf. Anders als Qwirbeln wird nichts archiviert und
nichts gelernt, der Chat bleibt einfach offen. Das Modell dafuer ist das
aus dem Chip, wie ueberall.

### Kleine Dinge, die stoerten

**Die fliegende Kopfleiste kam auch, wenn die echte noch zu sehen war.**
Sie misst jetzt gegen die Unterkante der echten Knopfzeile statt gegen
feste 200 Pixel - erst wenn die aus dem Bild ist, fliegt die zweite ein.

**Der Pfeil oben links klappte ohne Bewegung ein und sprang beim zweiten
Druck.** Jetzt wischen die Beschriftungen weg, dann gleitet die Leiste
schmal; beim Wechsel in die Kopfleiste bleibt sie schmal, waehrend sie
nach links wegfliegt, und wird erst breit, wenn sie unsichtbar ist. Vorher
wurde sie im selben Moment breit und weggeschoben - das war der Sprung.
Auf dem Rueckweg faden die Beschriftungen ein.

**Tabs wechseln jetzt sichtbar.** Ein kurzer Fade mit einem Hauch Bewegung
von unten, auch fuer die Chat-Reiter innerhalb eines Tabs. Wer Bewegung
im System abgestellt hat, bekommt wie bisher keine.

### Ein Gedaechtnis mit Index

**Qwirbel wusste nicht, was er weiss.** Sein Wissen lag in fuenf Ablagen,
ohne Verzeichnis. Also las er Dateien, statt sich zu erinnern. Jetzt gibt
es ein Gedaechtnis mit Faechern - Projekt, Entscheidung, Fehler, Regel,
Person, Hardware, Pfad, Werkzeug und beliebige eigene - und einen Index
mit einer Zeile je Erinnerung, der in jedem Lauf im festen Teil des
Prompts steht. Passt eine Zeile zum Auftrag, liest er die Erinnerung;
das kostet einen Bruchteil dessen, was das erneute Lesen der Dateien
kostet. Neues merkt er sich mit einem Werkzeug, und am Ende jeder
Aufgabe wird das Projekt-Fach von selbst fortgeschrieben: Datum, Auftrag,
was getan wurde, welche Dateien. Das alte Wissen bleibt, wo es ist - der
Index zeigt darauf.

## v2.9.7 - Was oben im Modellchip steht, rechnet. Ueberall.

### Der Modellchip

**Man konnte die Oberflaeche nicht uebersetzen lassen, obwohl das Modell
lief.** Ollama gestartet, oben ein lokales Modell gewaehlt, auf
"Uebersetzen" gedrueckt. Antwort: "Komplett-lokal-Modus ist an -
Cloud-Anbieter sind deaktiviert." Also eine Absage, die sich auf eine
Einstellung berief, die man selbst getroffen hatte - waehrend das Modell,
das man ausgewaehlt hatte, danebenstand und nichts zu tun hatte.

**Der Grund war, dass die Wahl im Chip nie das Programm erreicht hat.** Sie
lebte ausschliesslich im Browser und ging nur beim Chatten mit. Jede andere
Funktion - Uebersetzen, Benennen, Zusammenfassen, Einordnen - stand ohne sie
da und musste raten. Die Regel dafuer lautete: "irgendwo liegt ein aktiver
Cloud-Schluessel, also gehoert das in die API." Bei eingeschaltetem
Komplett-lokal-Modus fuehrte dieses Raten in eine Sackgasse, aus der es
keinen Ausweg gab: lokal verboten, Cloud verboten.

**Jetzt gibt es genau eine Stelle, die weiss, was im Chip steht.** Die
Oberflaeche meldet jede Aenderung dorthin, und der laufende Chat schreibt
zusaetzlich mit, womit wirklich gerechnet wurde - falls die Meldung des
Browsers einmal ausbleibt. Jede Funktion, die keine eigene Wahl mitbringt,
fragt dort nach, statt zu raten. Wer selbst eine Wahl hat, behaelt sie: ein
laufender Chat weiss besser als der Chip, womit er angefangen hat.

**Die Wahl gehoert dem Nutzer, nicht dem Rechner.** In einem Server-Paket
mit mehreren Menschen haette ein gemeinsamer Stand bedeutet, dass die
Modellwahl des einen bestimmt, womit die Uebersetzung des anderen rechnet -
und wer einen bezahlten Anbieter waehlt, laesst seinen Kollegen mitzahlen.
Jeder hat seinen eigenen Chip, wie jeder seine eigenen Chats hat.

**Nebenbei behoben: Umleitungen landeten beim falschen Anbieter.** Konnte
eine Nebenaufgabe nicht lokal laufen, ging sie an den ersten Eintrag der
Anbieterliste. Das ist Anthropic. Wer GLM gewaehlt und bezahlt hatte, bekam
so eine Rechnung bei Claude. Jetzt geht sie dorthin, wo der Nutzer
hinzeigt.

**Das automatische Einrichten stellt den Chip gleich mit.** Bisher setzte es
Modelle und Speicherprofil - und der Chip blieb leer. Frisch eingerichtet
stand das Uebersetzen der Oberflaeche also trotzdem ohne Wahl da, bis jemand
den Chip einmal von Hand angefasst hatte. Nur auf dem lokalen Weg und nur,
wenn das Modell wirklich installiert ist.

### Was eine Nachricht kostet

**Die Werkzeug-Beschreibung stand an der falschen Stelle im Prompt - und
das war teuer.** Sie ist 53.537 Zeichen lang, rund 14.900 Marken, und sie
aendert sich innerhalb einer Aufgabe kein einziges Mal. Nur stand sie hinter
Textstuecken, die sich bei jedem Schritt aendern. Ein Prompt-Cache arbeitet
aber ueber den ANFANG: was hinter etwas Veraenderlichem liegt, kann kein
Anbieter wiederverwenden. Bei dreissig Zuegen sind das rund 450.000 Marken,
jedes Mal neu bezahlt, obwohl Qwirbel das Caching laengst einschaltet. Jetzt
steht sie vorn, und sie wird einmal je Aufgabe gebaut statt bei jedem Zug.

**Dateien, die schon im Kontext stehen, werden nicht noch einmal
hineingeschrieben.** Es gab bereits einen Schutz gegen mehrfaches Lesen -
aber er sparte die falsche Haelfte. Er verhinderte den Zugriff auf die
Platte und schrieb den kompletten Dateiinhalt trotzdem erneut in den
Verlauf. Fuer das Modell ist das exakt derselbe Preis wie ein echtes Lesen:
gespart wurde eine Festplattenumdrehung, kein einziger Token. Und der Text
stand zu diesem Zeitpunkt schon zweimal im Prompt. Jetzt kommt an dieser
Stelle ein Zeiger von etwa vierhundert Zeichen. Bei einer Datei von
zwanzigtausend Zeichen, fuenfmal angefordert, sind das gut zweiundzwanzig-
statt hunderttausend Zeichen.

**Und "hat sich nicht geaendert" wird jetzt geprueft, statt behauptet.** Der
alte Satz stand da, ohne dass jemand nachgesehen hatte. Wer nebenher im
Editor speicherte, bekam still den alten Stand serviert. Aenderungszeit und
Groesse werden beim Merken festgehalten und beim naechsten Zugriff
verglichen; stimmt etwas nicht, wird wirklich neu gelesen.

**Ist der Kontext voll, wird jetzt zusammengefasst statt abgeschnitten.**
Bisher schnitt das Programm aeltere Zuege auf Kopf und Ende zurecht - und
das Ergebnis eines Zuges steht in der Mitte. Genau daher kam, dass der
Agent spaeter nicht mehr wusste, was er eigentlich getan hatte. Stattdessen
entsteht nun ein kurzes Protokoll: was fertig ist, was entschieden wurde,
welche Dateien angefasst sind, was offen ist und wo aufgehoert wurde. Am
Fenster aendert das nichts, dort stehen weiterhin alle Nachrichten - der
volle Wortlaut bleibt in der Chat-Datei und im Auto-Export.

**Gerechnet wird das im Hintergrund, mit Absicht.** Die Zusammenfassung
entsteht waehrend der Chat weiterlaeuft; bis sie da ist, gilt der bisherige
Schnitt. Ein Modellaufruf an dieser Stelle haette den Server mitten in der
Antwort fuer Sekunden angehalten. Ueber die API darf die Zusammenfassung
laenger sein, lokal wird sie knapp gehalten - dort zaehlt vor allem, was
passiert ist und wo es weitergeht. Scheitert das Modell daran, wird nichts
behauptet: dann greifen die bisherigen Kuerzungsstufen weiter.

**Der Agent bekommt eine gemessene Bilanz seiner eigenen Zuege.** Bisher
stand im Auftrag, was er selbst ueber seine Arbeit berichtet hatte - und
das hatte niemand nachgeprueft. Daneben steht jetzt eine kurze Liste aus
den Zuegen selbst: welche Datei geschrieben, welcher Befehl gelaufen ist,
was dabei herauskam. Wo beide auseinandergehen, gelten die Zuege. Fuenfzehn
Zeilen kosten ein paar hundert Marken; eine zum zweiten Mal geschriebene
Datei kostet Zehntausende.

### Oberflaeche

**Der Einstellungsknopf im Chat sagte "WORK".** Er ist seit der letzten
Fassung in allen Tabs zu finden, seine Ueberschrift kannte aber nur zwei
Faelle - Code oder alles andere. Im Chat stellte man also den Chat ein und
las dabei "Work". Jetzt nennt sie den Tab, in dem man steht, auf Deutsch
wie auf Englisch.

**55 Sprachen zum Anklicken.** Wer die Oberflaeche in einer weiteren
Sprache wollte, musste Kuerzel und Namen von Hand eintippen - und wer nicht
weiss, dass Ukrainisch "uk" heisst und nicht "ua", legte sie unter dem
falschen Kuerzel an und merkte es erst, wenn nach ueber sechzig
Uebersetzungsbloecken der Browser sie nicht erkannte. Jetzt steht die
Auswahl da, jede Sprache mit ihrem eigenen Namen; ein Klick legt sie an.
Das Eingabefeld bleibt fuer alles, was nicht dabei ist. Von rechts nach
links geschriebene Sprachen stehen bewusst nicht im Angebot: die Texte
liessen sich uebersetzen, die Oberflaeche steht danach aber falsch herum -
das waere ein Versprechen, das das Programm nicht haelt.

### Ordnung, Wissen, Installation

**Die Kratzordner raeumen sich auf - aber nichts verschwindet ohne
Rueckweg.** Unter `workspace/` sammeln sich Zwischendateien von
Agentenlaeufen, Browser-Aufnahmen, Bildschirmfotos und eingefuegte Bilder.
Niemand hat diese Ordner je angefasst; auf der Entwicklungsmaschine lagen
dort 1.786 Dateien und 153 MB. Jetzt wandert beim Start, was aelter als
30 Tage ist, in einen Papierkorb - und **erst der naechste Durchgang
loescht endgueltig, und auch der nur, was die Frist ein zweites Mal
ueberdauert hat.** Wer etwas vermisst, hat also mindestens einen Monat
Zeit, es zu holen. Bildschirmfotos und eingefuegte Bilder bleiben
unangetastet: die hat ein Mensch gemacht, die gehen nur auf ausdrueckliche
Ansage. Chats, Wissen, Einstellungen und die erzeugten Bilder und Videos
sind grundsaetzlich tabu.

**Qwirbel kann jetzt erklaeren, wie Qwirbel funktioniert.** Zum
mitgelieferten Wissen ist ein Blatt ueber das Programm selbst gekommen:
was die Tabs unterscheidet, was die Auswahl oben im Modellchip wirklich
bedeutet, warum "laeuft es hier" und "wer steuert den Motor" zwei
verschiedene Fragen sind, was beim Komprimieren des Kontexts passiert und
wo die Dateien liegen. Wer das Programm fragt, bekommt eine Antwort aus
dem Programm statt einer geratenen.

**Und mitgeliefertes Wissen erreicht jetzt auch eine BESTEHENDE
Installation.** Der Wissens-Ordner ist bei einem Update geschuetzt - zu
Recht, dort liegt alles, was eine Installation sich selbst erarbeitet hat.
Nur lag das MITGELIEFERTE Wissen im selben Ordner und war damit
mitgeschuetzt: ein neues Blatt kam nur bei einer frischen Installation an,
nie bei einem Update. Gemessen an genau diesem Fall - das neue Blatt lag im
Paket und fehlte danach in der Installation. Jede Verbesserung am
Kernwissen waere fuer alle Bestandskunden wertlos gewesen. Der mitgelieferte
Ordner ist jetzt ausdruecklich ausgenommen, auf beiden Update-Wegen; alles
daneben bleibt unantastbar.

**Die Setup-EXE sagt jetzt, ob sie aktualisiert oder neu installiert.**
Sie konnte beides immer schon, aber im Konsolenweg stand zwischen den
Trennlinien nichts - die Meldung kam von der Installationsstufe darunter
und ging verloren, sobald die Ausgabe umgeleitet oder mitgeschnitten wurde.
Wer die neue Fassung von der Website ueber seine Installation legt, liest
jetzt vor dem Kopieren, dass eine eingerichtete Installation gefunden
wurde, dass AKTUALISIERT wird und dass Chats, eigenes Wissen, Einstellungen
und Arbeitsordner unangetastet bleiben. Eine neue Pruefung stellt genau
diesen Fall nach - bestehende Installation mit eigenen Daten, neue EXE
darueber - und rechnet danach nach, was noch da ist.

**Zwei Dienste auf einem Port sagen jetzt, dass sie es sind.** Klecks
erwartet sich auf Port 8199. Wer ComfyUI von Hand auf dieselbe Nummer legt -
naheliegend genug, es ist ja Qwirbels eigene -, hat zwei Programme, die
denselben Platz wollen. Wer zuerst startet, gewinnt; der andere meldet
"antwortet nicht", und das sieht aus wie ein kaputter Dienst. Im
Auslieferungszustand kollidiert nichts (ComfyUI steht auf 8188), aber wenn
es passiert, steht es jetzt in der Meldung statt in einer stundenlangen
Suche.

## v2.9.6 - Warum bei Klecks nichts ging, und was jetzt passiert wenn er nicht kann

**Wer ein Klecks-Modell auswaehlte, bekam trotzdem Ollama.** Die Wahl hob
sich an zwei Stellen selbst auf. Erst setzte das Modell-Menue sie korrekt -
und ein Zuhoerer direkt daneben nahm sie sofort wieder zurueck, weil Klecks
ein lokaler Motor ist. Und beim Absenden ging fuer jeden lokalen Motor
`kein Anbieter` ans Programm, worauf dort der eingestellte Standardmotor
entschied; mitgeschickt wurde sogar Ollamas Modellname statt des
gewaehlten. Beides stammt aus der Zeit, als "lokal" schlicht "Ollama" hiess.
Seit es zwei lokale Motoren gibt, ist das falsch: wer Klecks waehlt, meint
Klecks. Massgeblich ist jetzt nur noch, ob es der Standardmotor ist.

**Und wenn man kein Klecks-Modell waehlt, bleibt alles bei Ollama und
ComfyUI.** Das ist die Vorgabe im Auslieferungszustand, und kein
Programmteil stellt sie je von selbst um - ein Test wacht darueber. Bilder
laufen ohnehin immer ueber ComfyUI: Klecks ist ein Sprachmotor und wird in
der Bilderzeugung nirgends aufgerufen.

**"Keine Modelle gemeldet - laeuft der Dienst?" - der Dienst lief.** Diese
Meldung war geraten, und sie hat wochenlang in die falsche Richtung
gezeigt. Gemessen auf der Entwicklungsmaschine: der Klecks-Dienst
antwortete einwandfrei mit 22 Sprachmodellen, brauchte dafuer beim ersten
Mal aber 20,8 Sekunden - er liest je Modell den Dateikopf. Qwirbel wartete
15 Sekunden. Jeder Aufruf lief also in die Zeitueberschreitung, und ein
`ausser: nichts zurueckgeben` warf den Grund weg. Zusammen mit dem Umstand,
dass die Liste frueher nur einmal beim Fensterstart geholt wurde, blieb
Klecks damit dauerhaft leer.

**Jetzt darf die Liste 90 Sekunden brauchen, und der Grund wird gesagt.**
Zu langsam ist etwas anderes als nicht erreichbar, und beides ist etwas
anderes als "keine Modelle da". Alle drei Faelle haben jetzt ihren eigenen
Satz, und der steht dort, wo vorher die Vermutung stand. Eine geratene
Ursache ist schlimmer als gar keine: sie schickt Menschen auf die falsche
Faehrte.

**Kann Klecks nicht, uebernimmt Ollama - und man sieht es.** Bisher flog
ein Klecks-Fehler durch und die Antwort blieb einfach aus. Jetzt rechnet
Ollama weiter, und im Chat steht die Zeile "Anbieter gewechselt: Klecks ->
Ollama" mit dem Grund zum Draufzeigen. Dasselbe gilt fuer Agentenlaeufe -
dort steht es im Protokoll, weil ein Agent diese Chat-Zeile nicht hat.

**Eine Ausnahme, und die ist wichtig: wer selbst auf Stopp drueckt, bekommt
keinen Ersatzlauf.** Ein Rueckfall waere dort das Gegenteil dessen, was der
Mensch gerade gedrueckt hat - und die teuerste Art, ihn zu ignorieren.

**Und noch ein "Python", das eigentlich Qwirbel ist: der Klecks-Dienst.**
Er wurde mit dem pythonw.exe aus dem Scripts-Ordner gestartet - und das ist
unter Windows nur ein Starter, der den echten Interpreter als zweiten
Prozess aufruft. Zwei Eintraege im Taskmanager, beide namenlos, beide
gehoeren zu Qwirbel. Jetzt laeuft er unter derselben beschrifteten Kopie -
aber nur, wenn der gewaehlte Interpreter in Qwirbels eigener Umgebung
liegt. Zeigt er woandershin (Klecks' eigene Umgebung, ein von Hand
eingetragener Pfad), bleibt er unangetastet: dort waere ein Tausch ein
stiller Unterschied zwischen "bei mir lief es" und "beim Nutzer nicht".

**Zwei Reste des Colibri-Fehlers waren noch da.** Der LOKAL/API-Schalter
suchte seine API-Anbieter, indem er "ollama" und "klecks" bei NAMEN
aussortierte - Colibri und Kimi laufen aber auch auf diesem Rechner und
standen deshalb als API-Anbieter in der Liste. Und in der Agenten-Anzeige
stand bei ihnen "ueber deinen API-Schluessel - Grafikkarte bleibt frei".
Beides falsch: sie rechnen auf genau dieser Karte, und es geht kein
Schluessel ins Netz. Eine Aussage ueber Datenschutz und Grafikkarte darf
nicht geraten werden.

**"Ist das lokal?" und "ist das der Standard?" sind zwei Fragen.** Beide
standen im Programmtext als derselbe Vergleich mit dem Wort "ollama", und
an dem war nicht zu erkennen, welche gemeint war. Genau diese Verwechslung
hat GLM Colibri monatelang zum API-Anbieter gemacht. Die zweite Frage hat
jetzt einen eigenen Namen, der sie ausspricht - der blanke Vergleich steht
nirgends mehr.

**Der Taskmanager-Name haelt jetzt auch unter Last.** Windows laesst das
Beschriften einer frisch geschriebenen Datei fehlschlagen, solange ein
Virenscanner sie noch anfasst. Beim ersten Fehlversuch aufzugeben hiess:
der Nutzer sieht wieder "Python" und weiss nicht warum. Jetzt sind es drei
Anlaeufe, und beim naechsten Start wird es ohnehin erneut versucht.

## v2.9.5 - Qwirbel heisst Qwirbel, und das Logo bleibt

**Im Taskmanager stand weiterhin "Python".** In v2.9.2 wurde dagegen eine
byte-gleiche Kopie von `pythonw.exe` unter dem Namen `Qwirbel.exe`
angelegt. Gemessen bringt das nichts: Windows zeigt dort nicht den
Dateinamen, sondern die BESCHREIBUNG aus der Versions-Ressource der Datei -
und die sagte in der Kopie unveraendert "Python". Ein Name, der nur im
Explorer stimmt und an der Stelle nicht, um die es ging.

**Und es war der falsche Interpreter.** Unter Windows ist
`.venv\Scripts\pythonw.exe` kein Interpreter, sondern ein Starter von 263
Kilobyte, der den echten (104 Kilobyte) als EIGENEN Prozess nachruft.
Kopiert wurde der Starter. Im Taskmanager standen deshalb je Lauf zwei
Eintraege, und der, der wirklich rechnet, hiess nie Qwirbel - genau der
zweite Eintrag, den man dort sah.

**Jetzt wird der echte Interpreter kopiert und beschriftet.** Qwirbel
schreibt eine eigene Versions-Ressource hinein (Beschreibung und Produkt =
Qwirbel, dazu die Versionsnummer) und ersetzt das Symbol durch das
Qwirbel-Logo in allen neun Groessen bis 256 Pixel. Weil die Datei im
Scripts-Ordner liegt, benutzt sie dieselbe Umgebung wie zuvor -
nachgemessen: derselbe Interpreter, dieselben Pakete, aber ein Prozess
weniger und der richtige Name. Windows kann das selbst, es kam keine
Bibliothek dazu. Klappt es nicht (kein Schreibrecht, Virenscanner), startet
Qwirbel wie immer und nur der Name bleibt Pythons: ein falscher Name ist
ein Schoenheitsfehler, ein nicht startendes Programm nicht.

**Nach einem Update war das Desktop-Logo weg und die Startmenue-Anbindung
nicht mehr richtig.** Das Update legt `frontend/qwirbel.ico` neu ab. Die
Verknuepfung zeigt weiter auf denselben Pfad - aber Windows hat das Bild
darunter zwischengespeichert und zeigt danach das alte oder gar keins. Der
Explorer merkt von sich aus nichts davon, denn fuer ihn hat sich die
Verknuepfung nicht geaendert.

**Jetzt frischt Qwirbel die Verknuepfungen nach jedem Update selbst auf**
und sagt dem Explorer Bescheid. Zwei Regeln sind dabei wichtiger als das
Symbol: Es werden NUR vorhandene Verknuepfungen angefasst - wer beim
Einrichten keine wollte, bekommt durch ein Update keine. Und nur die, die
auf DIESE Installation zeigen - wer eine zweite Kopie woanders betreibt,
dessen Verknuepfung bleibt unberuehrt.

## v2.9.4 - Was da steht, tut jetzt auch etwas

**"Lokal" hiess an siebzehn Stellen im Programm etwas anderes.** Das klingt
nach einer Kleinigkeit und war der Grund fuer mehrere Fehler, die sich
monatelang gehalten haben. Der wichtigste: GLM Colibri lief die ganze Zeit
auf dem eigenen Rechner, wurde aber ueberall als API-Anbieter gefuehrt -
in der Anzeige, bei der Schluessel-Pflicht, in der Datenschutz-Einordnung.
Der zweite: sobald ein paar API-Schluessel hinterlegt waren, war "lokal"
keine echte Option mehr. Man konnte den Schalter "komplett lokal"
anschalten und Ollama auswaehlen, und Qwirbel meldete trotzdem, die API
sei aus.

**Dahinter steckten zwei verschiedene Fragen, die nie sauber getrennt
waren.** Die eine lautet: laeuft dieser Anbieter auf diesem Rechner? Davon
haengen Anzeige, Schluessel-Pflicht, Datenschutz und die Ausweich-Kette ab.
Die andere lautet: welcher Motor rechnet ihn? Davon haengt ab, welcher
Programmteil ihn faehrt. Colibri antwortet auf beide verschieden - er
laeuft hier, wird aber ueber den OpenAI-Weg gefahren. Beide Fragen haben
jetzt je eine Funktion mit einer Antwort, und ueberall im Programm wird
die passende gestellt statt Namen zu vergleichen.

**Ein Chat, den man fuer lokal hielt, konnte still in die Cloud fallen.**
Gemessen vor der Behebung: wer Colibri gewaehlt hatte, dessen Anfrage ging
beim ersten Schluckauf weiter an Anthropic, Google und z.ai. Bei Kimi ging
sie sogar sofort dorthin, ohne es ueberhaupt bei Kimi zu versuchen. Das war
kein Schoenheitsfehler, sondern ein Datenschutz-Leck. Lokale Anbieter
weichen jetzt nur noch auf lokale aus.

**Bilder gehen im Chat wieder, auch mit einem Cloud-Modell.** War ein
Anbieter ohne Agenten-Faehigkeit gewaehlt, fing ein Zweig jede Nachricht ab
und machte reinen Text daraus - eine Bitte wie "mach mir ein Bild von einer
Katze" kam nie bei ComfyUI an. Dabei laeuft die Bilderzeugung ohnehin
lokal und hat mit dem Chat-Anbieter nichts zu tun.

**Zwei Knoepfe im Programm taten gar nichts.** Wer ein PDF, ein Word- oder
Excel-Dokument in den Chat zog, bekam "konnte nicht gelesen werden". Der
Leser dafuer war seit Wochen fertig eingebaut - nur der Weg vom Browser
dorthin fehlte, der Aufruf lief ins Leere. Und der orangene Punkt in der
Kopfleiste, der ein bereitliegendes Update anzeigen soll, fragte alle
fuenfzehn Minuten eine Adresse ab, die es nicht gab. Er ist nie
erschienen, auch wenn ein Update bereitlag. Beide Wege sind jetzt gebaut.

**Damit so etwas nicht wieder unbemerkt bleibt, prueft ein Test jetzt alle
282 Aufrufe, die die Oberflaeche kennt, gegen die 384 Adressen des
Programms.** Ein Knopf, der ins Leere greift, faellt ab sofort beim Bauen
auf und nicht beim Kaeufer.

**Ein frisch geladenes Modell erschien erst nach einem Neustart.** Die
Liste im Chat-Chip wurde genau einmal beim Oeffnen des Fensters geholt. Wer
sich im Models-Tab ein Modell zog, suchte es danach vergeblich - der Chip
wirkte kaputt. Jetzt meldet jeder fertige Download sich selbst, und beide
Listen, Ollama und Klecks, ziehen sofort nach.

**Modelle werden nicht mehr wegen des Kontext-Fensters ausgegraut.** In
einem laengeren Gespraech fiel eines nach dem anderen aus der Auswahl, bis
gar nichts mehr waehlbar war. Die Information ist geblieben, aber als
Hinweis am Knopf statt als Schloss. Ausgegraut wird nur noch, was fuer
Work und Code zu klein ist - und diese Grenze setzt man selbst.

**Der Ein/Aus-Schalter eigener Anbieter war eine Einbahnstrasse.** Er war
gesperrt, solange kein Schluessel eingetragen war. Ein eigener Server auf
dem gleichen Rechner braucht keinen - einmal ausgeschaltet, liess er sich
nie wieder anschalten.

**Der Workflow-Import bot sieben Arten an und speicherte vier davon.** Wer
einen LTX-Workflow importierte und "Text zu Video" auswaehlte, bekam ein
freundliches "gespeichert" und die Angabe war weg. Qwirbel fand den
Workflow danach nie wieder von selbst. Dasselbe galt fuer Stimme und
Motion-Control.

**"Modell an einen Chat binden" ist aus Work und Code raus.** Der Schalter
versprach, dass ein Chat bei seinem Anbieter bleibt, bewirkte aber nur
eine Warnung beim Wechsel - also weder das, was sein Name sagte, noch das,
was gemeint war.

**Fuenf Fehlermeldungen im Protokoll bestanden aus einer Zeichenkette statt
aus dem Fehler,** und fuenf Ausnahme-Faenge haetten beim Zuschlagen selbst
einen Fehler ausgeloest: sie wollten einen Fehler ausgeben, der an dieser
Stelle gar nicht gesetzt war. Aus einem verschluckten Schoenheitsfehler
waere dort ein echter Absturz geworden. Ein neuer Test geht ueber alle 137
Programmdateien und findet Namen, die es zur Laufzeit nicht gibt - etwas,
das der uebliche Syntax-Check nicht sieht.

**Klecks wurde an sechs Stellen wie ein Cloud-Anbieter behandelt,** obwohl
er auf derselben Grafikkarte rechnet. Unter anderem versprach der
Schwarm-Vorschlag viele gleichzeitige Agenten fuer ihn, die sich in
Wirklichkeit dieselben sechzehn Gigabyte geteilt haetten. Und wer Klecks
als lokalen Motor einstellte, ohne im Chat noch einmal ausdruecklich zu
waehlen, landete trotzdem bei Ollama - der Schalter tat nichts.

## v2.9.3 - Qwirbel hoert wieder sofort zu

**In v2.9.1 ist beim Aufraeumen ein Fehler hereingekommen, und der hat
ausgerechnet das Zuhoeren getroffen.** Auf dem Anmeldeschirm hatte Qwirbel
im Sekundentakt versucht, seine Live-Verbindung aufzubauen, obwohl noch
niemand angemeldet war. Dagegen wurde eine Wartezeit eingebaut, die sich
nach jedem Fehlversuch verdoppelt. Das war zu grob gedacht: sie wuchs bis
auf dreissig Sekunden, und ueber genau diese Live-Verbindung kommen auch
Diktat und Hotword. Wer den Diktat-Knopf drueckte, wurde deshalb unter
Umstaenden erst nach zehn bis siebzehn Sekunden verstanden. Gemessen auf
dieser Maschine: Verbindungsversuche bei 1,6 - 3,7 - 8,6 - 17,6 Sekunden.

**Jetzt gilt ein Deckel von fuenf Sekunden, und jede Beruehrung hebt die
Wartezeit sofort auf.** Wer zum Fenster zurueckkommt, es anklickt oder
tippt, ist wieder verbunden, bevor der Finger unten ist - gemessen eine
Millisekunde nach dem Klick. Der Schutz gegen das Dauerfeuer auf dem
Anmeldeschirm bleibt, er trifft nur nicht mehr den Menschen davor.

## v2.9.2 - Aufgeraeumt, und drei Zahlen, die man selbst setzen kann

**Im Verkaufspaket lagen 215 Dateien, die niemanden ausser dem Entwickler
etwas angehen.** Die komplette Testsuite mit ihren einhundertachtundzwanzig
Dateien, der Werkzeugkasten zum Uebersetzen der Oberflaeche, Bau- und
Deploy-Skripte, interne Befunde und Code-Reviews - und die Anleitung, wie
man Qwirbel-Pakete selbst baut. Das Paket schrumpft damit von 898 auf 683
Dateien. Geprueft wurde vorher, dass nichts davon zur Laufzeit gebraucht
wird: jeder Verweis darauf im verbleibenden Paket steht in einem Kommentar,
nicht in einem Aufruf.

**Im Taskmanager stand "Python".** Windows zeigt dort den Dateinamen des
Programms, und der war nun mal Pythons. Jetzt liegt neben dem Interpreter
eine gleiche Kopie namens Qwirbel.exe, und im Taskmanager steht, was
laeuft. Es ist derselbe Interpreter unter anderem Namen, kein zweiter - die
Umgebung bleibt dieselbe. Die Kopie entsteht beim Start selbst, bestehende
Installationen bekommen den Namen also ohne neues Setup.

**Neu: eine eigene Untergrenze fuer MCP-Werkzeuge.** Ein kleines Modell
bekommt mit zugeschalteten MCP-Servern eine zweite, fremde Werkzeugliste in
den Prompt - es hat mit der eigenen schon genug zu tun und faengt an,
Aufrufe zu erfinden. In den Einstellungen steht jetzt eine eigene Zahl:
unter so vielen Milliarden Parametern gibt es in Work und Code keine
MCP-Werkzeuge. Standard 30, 0 schaltet die Regel ab. Bewusst eine EIGENE
Zahl neben der Modell-Untergrenze: die eine entscheidet, wer den Reiter
ueberhaupt fahren darf, die andere nur ueber MCP. Ist die Groesse eines
Modells nicht zu ermitteln, wird nicht gesperrt - eine stille Sperre waere
schlimmer als ein Modell, das einmal zu viele Werkzeuge sieht.

**Und wieviele Nachrichten der Chat im Gedaechtnis hat, laesst sich jetzt
einstellen.** Das war eine feste Zwoelf im Programmtext, an die ohne
Code-Aenderung niemand herankam. Jetzt steht sie in den Einstellungen,
Standard fuenfzehn. Das ist Qwirbels Kurzzeitgedaechtnis: "mach noch eins"
funktioniert nur, wenn genug davon drin ist - mehr kostet aber bei jeder
Antwort Marken.

## v2.9.1 - Qwirbel ist beim Oeffnen da, nicht nach dem Ladekreis

**Beim Start kamen fuenf Megabyte ueber die Leitung, jetzt sind es 624
Kilobyte.** Qwirbel schickte seine Oberflaeche bisher als ein einziges,
unuebersetztes Stueck an den Browser - 1,9 Megabyte - und dazu noch den
Uebersetzer selbst, weitere 2,7 Megabyte. Der Browser musste damit bei jedem
Oeffnen rund dreissigtausend Zeilen neu uebersetzen, bevor das erste Bild
stand. Diese Uebersetzung passiert seit v2.8.7 eigentlich schon beim Bauen -
sie kam nur nie beim Kunden an, weil beim Packen ein Erkennungszeichen nicht
mehr zum Inhalt passte und Qwirbel deshalb sicherheitshalber den alten,
langsamen Weg nahm. Das ist behoben. Gemessen auf dieser Maschine: die Seite
ist nach **102 Millisekunden** benutzbar statt nach **2670**.

**Und alles wird jetzt komprimiert ausgeliefert.** Bisher ging jede Antwort
unverpackt raus. Jetzt werden Oberflaeche, Programmteile und Schriften
gepackt - dieselben Daten, rund siebzig Prozent weniger Leitung. Der
Live-Text im Chat ist davon bewusst ausgenommen: der soll Wort fuer Wort
tropfen, nicht gesammelt ankommen.

**Das Hintergrundbild wurde bei jedem Fensteroeffnen komplett neu geladen.**
Wer ein Video als Hintergrund gewaehlt hat, zahlte das besonders teuer - im
Test ein Film von 51 Megabyte, jedes Mal aufs Neue. Qwirbel sagte dem
Browser woertlich, er duerfe die Datei nicht behalten. Jetzt darf er sie
behalten und fragt nur kurz nach, ob sie noch aktuell ist: unveraendert
kostet sie **null Byte**. Ein gewechselter Hintergrund erscheint trotzdem
sofort - daran aendert sich nichts.

**Das zweite Oeffnen ist jetzt fast leer.** Programmteile bekommen eine
Adresse, die sich mit ihrem Inhalt aendert. Damit darf der Browser sie
dauerhaft behalten und holt beim naechsten Mal gar nichts mehr - der lange
Kreis beim Fensteroeffnen faellt weg. Aendert ein Update etwas, aendert sich
die Adresse und es wird von selbst neu geholt.

**Die Handy-App holt sich nichts mehr doppelt.** Ihr Hintergrunddienst
reichte bisher jede einzelne Anfrage nur durch, um sie danach genauso ans
Netz zu geben - ein Umweg pro Datei, ohne Nutzen. Der ist weg; die App
bleibt installierbar wie bisher.

**Kleinigkeit am Rande:** Auf dem Anmeldeschirm versuchte Qwirbel im
Sekundentakt, seine Live-Verbindung aufzubauen, obwohl noch niemand
angemeldet war - achtzehn Versuche in gut einer Minute. Jetzt wartet er
zwischen den Versuchen immer laenger. Ein echter Neustart im Hintergrund
wird weiterhin binnen einer Sekunde bemerkt.

## v2.9.0 - Eine Entscheidung, ein Weg, ein Takt

**Qwirbel hat an vielen Stellen dieselbe Frage verschieden beantwortet.** Wer
antwortet auf diese Anfrage - die Cloud, dein eigener Klecks, das lokale
Ollama? Diese Frage wurde bisher an mehreren Orten im Programm getrennt
entschieden, jeder mit seinen eigenen Wenn-Dann-Zweigen. Das ging lange gut und
irgendwann nicht mehr: Klecks wurde an einer dieser Stellen als Cloud-Dienst
eingeordnet und bekam deshalb das Cloud-Limit statt des lokalen - obwohl er auf
deinem eigenen Rechner rechnet. Jetzt gibt es EINE Weichenstelle, die pro
Anfrage einmal entscheidet, und alle anderen fragen dort nach. Was erlaubt ist,
sagt weiterhin dieselbe Stelle wie bisher; es entsteht keine zweite Regel
daneben.

**Antworten kamen auf zwei verschiedenen Wegen herein.** Eine Antwort, die Wort
fuer Wort erscheint, und eine, die am Stueck ankommt, liefen durch getrennten
Code - mit dem Ergebnis, dass Ende, Fehler und Abbruch je nach Weg und je nach
Motor unterschiedlich behandelt wurden. Beide teilen sich jetzt dieselbe
Schleife. Eine abgebrochene Antwort verhaelt sich bei jedem Motor gleich, und
offene Verbindungen werden zugemacht, statt irgendwann von selbst auszulaufen.

**Der Stop-Knopf hat gebeten, nicht gestoppt.** Ein laufender Lauf wurde
angehalten, indem das Programm hoeflich fragte - die Verbindung selbst lief
weiter. Jetzt wird sie wirklich abgebrochen. Dazu kommt ein Zeitwaechter: wenn
im Antwortstrom laengere Zeit gar nichts mehr passiert, bricht Qwirbel von
selbst ab, statt dich vor einem Kreisel sitzen zu lassen, hinter dem nichts
mehr kommt.

**Der Denk-Kreisel blieb manchmal haengen.** Wer waehrend einer laufenden
Antwort den Reiter oder den Motor wechselte, sah unter Umstaenden dauerhaft
einen arbeitenden Qwirbel, obwohl nichts mehr lief. Der Chat hat jetzt einen
klaren Zustand - leer, laedt, antwortet, fehler, abgebrochen - und ein Wechsel
setzt ihn hart zurueck. Ein haengengebliebenes Stueck Antwort kann den Zustand
nicht mehr faelschen.

**Dutzende Uhren liefen unabhaengig voneinander, auch unsichtbar.** Dienststatus,
Grafikspeicher, Modellbelegung, Downloads, Token-Zaehler - jede Anzeige fragte
in ihrem eigenen Takt nach, auch dann, wenn ihr Reiter gar nicht zu sehen war.
Bei jedem Reiterwechsel summierten sich diese Abfragen. Jetzt gibt es einen
gemeinsamen Takt: ist das Fenster nicht sichtbar, pausiert er ganz, und beim
Zurueckkommen holt jede Anzeige genau einmal den frischen Stand nach statt einen
Stau abzuarbeiten.

**Und Qwirbel verschweigt keine uebersprungenen Fehler mehr.** An
einhundertsieben Stellen wurde ein Fehler bisher stumm geschluckt - fuer dich
sah das aus, als sei nichts passiert, obwohl etwas nicht geklappt hatte. Diese
Stellen sagen jetzt, was sie uebersprungen haben. Drei Faelle sind dabei
besonders aufgefallen und wurden ehrlich gemacht: ComfyUI wurde mit einem
geratenen Port angesprochen, wenn in den Einstellungen keiner stand; ein
fehlender Arbeitsablauf fuer Video oder Musik wurde still durch einen anderen
ersetzt (du bekamst ein Ergebnis, nur nicht das gemeinte); und eine fehlende
LoRA-Datei wurde durch eine aehnlich klingende ersetzt. Alles drei meldet sich
jetzt mit einem klaren Grund, statt heimlich etwas anderes zu tun.

## v2.8.9 - Symbole, die etwas sagen, und ein Regler, der richtig rechnet

**Auf jeder Stufe stand dasselbe Maennchen.** Ob "Blitz" oder "Maximal", ob im
Chat oder im Code-Reiter - der Regler fuer Muehe und der fuer Rechte zeigten
ueberall dieselbe Pixelfigur. Sie sagte weder etwas ueber die Stufe noch
darueber, was der Reiter eigentlich tut. Jetzt traegt jede Stufe ein eigenes
Symbol, und jeder Reiter seine eigene Bildsprache: der Chat geht vom Blitz
ueber die Sprechblase und die Lupe zum Gehirn, der Code-Reiter erzaehlt den
Bau-Ablauf selbst - hinschreiben, starten, testen, Kaefer fangen, im laufenden
Programm klicken, reparieren. Die Rechte-Stufen folgen dem, was sie erlauben:
Stufe 2 heisst "Arbeitsordner" und zeigt einen Ordner, Stufe 7 heisst
"Aufraeumen" und zeigt einen Besen. Das Maennchen ist nicht verschwunden - es
wackelt weiter im Chat, solange gearbeitet wird.

**Und ein Arm des Maennchens lief quer.** Beide Arme drehten sich um denselben
Punkt und in dieselbe Richtung: der eine schwang nach aussen, der andere quer
ueber den Koerper. Schuld war eine fehlende Angabe, worauf sich die Drehung
bezieht - ohne sie nahm der Browser die Mitte des ganzen Bildes statt die
Schulter des jeweiligen Arms. Beide Arme kreisten also um den Kopf. Jetzt hat
jede Seite ihren eigenen Drehpunkt und ihre eigene Richtung.

**Die Modell-Schranke rechnete nach jedem Chatwechsel mit null.** Qwirbel graut
Modelle aus, die fuer einen Chat zu klein sind - das haengt daran, wie voll der
Verlauf schon ist. Diese Zahl wurde aber aus der Anzeige "zuletzt gesehener
Reiter" geholt. Passte die nicht zum Reiter, in dem man gerade stand, setzte
Qwirbel den Verlauf auf null und die Schranke griff nicht. Eine zweite Stelle -
das Zahnrad in Work und Code - fragte gar nicht erst nach, welcher Reiter
gemeint ist, und rechnete mit dem Verlauf eines fremden Chats. Beide holen den
Wert jetzt dort, wo er nach Reitern getrennt liegt.

**Das Modell-Menue liess auf sich warten.** Es fragte erst beim Aufklappen nach,
welche Modelle taugen - und dahinter stehen zwei Anfragen an Ollama und Klecks,
die bis zu fuenf Sekunden brauchen duerfen. So lange stand das Menue
ungefiltert da. Der letzte Stand wird jetzt je Reiter gemerkt und ist sofort da;
nachgefragt wird im Hintergrund.

**Ein erzeugtes Video blieb im Generieren-Reiter schwarz.** Dort konnte die
Anzeige nur Bilder. Wer ein Video oder ein Musikstueck erzeugte, bekam es in
ein Bild-Feld gelegt - im Chat war dasselbe Ergebnis in Ordnung. Es gab zwei
getrennte Anzeigen fuer dieselbe Sache. Jetzt ist es eine, und der
Generieren-Reiter kann Filme und Ton wie der Chat.

**Angehaengte Bilder gingen zwei verschiedene Wege.** Ein reingezogenes Bild
wurde anders angezeigt als ein mit Strg+V eingefuegtes - unter anderem liess
sich nur eines davon zum Vergroessern anklicken. Beide laufen jetzt durch
dieselbe Anzeige, egal ob das Bild als Datei oder als Pfad ankommt.

**Mehrere laufende Auftraege liessen sich nicht einklappen.** Wer in zwei
Reitern gleichzeitig arbeiten liess, bekam zwei volle Schrittlisten
untereinander und musste durch alles hindurchscrollen. Das war kein Zufall,
sondern Rechnung: die Spalte darf nicht ganz so hoch werden wie das Fenster,
jedes einzelne Panel aber fast halb so hoch - zwei passen also nie zusammen
hinein. Jedes Panel laesst sich jetzt einzeln zuklappen und merkt sich das;
eingeklappt bleiben Titel, Fortschritt, Zustand und der Schritt sichtbar, der
gerade laeuft. Laufende Auftraege stehen oben, fertige rutschen nach unten.

**Im Taskmanager stand "pythonw.exe" mit dem Python-Logo.** Qwirbel laeuft als
Python-Programm, und genau das stand auch im Taskmanager - fuer ein gekauftes
Programm sieht das aus wie ein fremder Interpreter. Jetzt startet Qwirbel als
"Qwirbel.exe" mit dem eigenen Symbol, in neun Groessen bis 256 Pixel. Das ist
kein Umweg ueber ein zusaetzliches Startprogramm: es ist derselbe Interpreter,
nur unter eigenem Namen und mit eigenem Bild. Auch das Fenster laeuft jetzt
darunter. Faellt die Datei weg, startet Qwirbel wie bisher weiter.

**Das Tray-Menue hatte drei Eintraege.** Oeffnen, Browser, Beenden - alles
andere ging nur ueber das Fenster, auch wenn man es gar nicht sehen wollte.
Dazugekommen sind: Grafikspeicher freigeben (der Knopf, den es bisher nur in
der Oberflaeche gab - praktisch, wenn man schnell zocken will), Programm-,
Arbeits- und Protokollordner oeffnen sowie Neu starten. Der Neustart geht
ueber den richtigen Startweg, nicht am Programmordner vorbei.

**Unten im Chat liessen sich die lokalen Modelle nicht waehlen.** Der
Anbieter-Knopf zeigte die Modell-Liste nur bei Cloud-Anbietern; wer Ollama
fuhr, sah nur die Anbieter, und das Menue schloss sich beim Klick sofort
wieder. Das Modell liess sich nur oben im Kopf wechseln. Jetzt zeigt der Knopf
in beiden Faellen dieselbe Liste - und beide Wege stellen dieselbe Wahl,
nicht zwei getrennte.

**Und die Werkzeug-Listen darin waren zu lang, um sie zu lesen.** In einem
einzigen Auftrag sind ueber dreihundert Werkzeug-Zeilen zusammengekommen -
gekuerzt hat sie niemand, weder der Server noch die Anzeige. Sichtbar war davon
etwa ein Zehntel, der Rest lag im Scrollbereich. Jetzt zeigt der laufende
Schritt seine letzten sechs Werkzeuge, ein abgehakter seine letzten zwei, und
darueber steht, wie viele es sonst noch waren.

## v2.8.8 - Knoepfe, die nichts taten, tun jetzt etwas

**Der Knopf "Mehr" hat die Oberflaeche zerlegt.** Wer in der schlichten
Ansicht oben auf "Mehr" drueckte, bekam statt der Tab-Liste einen Fehlerschirm:
"Qwirbel hat einen Schluckauf". Der Grund war eine einzige fehlende
Weitergabe - das Menue wollte wissen, in welchem Reiter man gerade steht,
bekam es aber nie gesagt und stuerzte bei jedem Oeffnen ab. Deshalb hat auch
die Gruppe "Hier bist du" nie funktioniert, die genau das zeigen sollte.

**Zehn Bedienwege brachen still ab.** Beim Umbau der aufklappbaren Reiter am
12.08. wurde ein Schalter entfernt - zehn Aufrufe blieben stehen. Jeder von
ihnen warf einen Fehler, und weil er MITTEN in der Zeile stand, lief der Rest
der Zeile nicht mehr. Betroffen waren: die Tastenkuerzel zum Reiter-Wechsel,
das Hotword "Hey Qwirbel", das Diktat in die Planung, der Weg aus dem Chat in
den Code-Reiter und der Knopf "Browser koppeln". Der Reiter wechselte, der
Unterreiter blieb stehen - und niemand konnte sagen, warum. Eine neue Pruefung
faengt genau diese Fehlerart ab jetzt vor dem Bauen ab; sie hat die beiden
Stellen gefunden.

**Ein Druck aufs Logo holt das Fenster zurueck.** Bisher stand da ein Zettel:
"Qwirbel laeuft bereits - bitte dieses Fenster benutzen, es ist vielleicht
hinter einem anderen." Ein Programm, das weiss, wo sein Fenster ist, soll es
holen und nicht beschreiben. Dasselbe im Tray: "Qwirbel oeffnen" und das
Tastenkuerzel Strg+Shift+Q taten gar nichts, solange das Fenster lief - sie
holen es jetzt nach vorn.

**Der Knopf "Jetzt installieren" war unsichtbar, obwohl das Paket bereitlag.**
Seit 2.8.6 sucht Qwirbel das Update je Betriebssystem im passenden Eintrag.
Der Knopf fragte aber noch das alte, gemeinsame Feld ab - wer das Verzeichnis
richtig ausfuellte, bekam den Knopf nie zu sehen. Jetzt entscheidet der Server,
ob es fuer DIESEN Rechner ein Paket gibt, und zwar mit derselben Funktion, die
es danach auch herunterlaedt.

**Ein Update sagt jetzt Bescheid.** Liegt eine neue Fassung bereit, sitzt ein
oranger Punkt am Zahnrad oben, und im Menue darunter steht, welche Version es
ist. Dazu kommt einmal ein kleines Fenster unten rechts - einmal je Version,
nicht bei jedem Start. Es blockiert nichts. Der Punkt bleibt, bis das Update
da ist.

**Der Pfeil oben links hat drei Stufen.** Volle Seitenleiste, nur Symbole,
Kopfleiste oben - und aus der Kopfleiste fuehrt derselbe Pfeil an derselben
Stelle wieder zurueck. Vorher war das Umschalten zwischen den beiden Ansichten
nur ueber die Einstellungen erreichbar.

**Welcher Reiter vorne steht, laesst sich endlich einstellen.** Das ging bisher
nur ueber einen Rechtsklick im "Mehr"-Menue - wer das nicht zufaellig
ausprobiert hat, fand es nie. Unter Einstellungen -> Menue steht es jetzt bei
Sortieren und Ausblenden, mit dem Hinweis, was fuer beide Ansichten gilt und
was nur fuer die schlichte.

**Die Update-Historie zeigte Unsinn.** Nach jedem Update standen dort zwei
Zeilen statt einer, und die zweite behauptete einen Wechsel von einer Version
auf sich selbst. Als Paketname stand ein Zufallsname aus dem Zwischenspeicher
statt der Datei, die man ausgewaehlt hatte. Beides sind jetzt eine Zeile und
der richtige Name.

**In jedem verkauften Paket lagen 861 Dateien, die dort nicht hingehoerten.**
Vorschaubilder erzeugter Bilder, Zwischenstaende laufender Auftraege und der
Update-Verlauf des Rechners, auf dem gepackt wurde - zusammen rund 14 Megabyte
in jedem Paket, auf allen drei Betriebssystemen. Das Windows-Paket schrumpft
damit von 28,8 auf 15,6 Megabyte. Neue Kaeufer sahen im Update-Tab bisher eine
fremde Historie.

**Vorbereitet: Updates werden klein.** Statt des ganzen Programms kann Qwirbel
kuenftig nur noch die geaenderten Dateien laden - gemessen 2,2 statt 15,6
Megabyte, mit demselben Ergebnis Datei fuer Datei. Das ist gebaut und geprueft,
aber noch nicht in Betrieb: dafuer muss die Bezugsquelle erst umgestellt
werden. Bis dahin bleibt alles wie gewohnt.


## v2.8.7 - Qwirbel startet in Sekunden statt in einer halben Minute

**Das Programm hat sich bei jedem Oeffnen selbst neu uebersetzt.** Die
Oberflaeche ist ein einziges grosses Stueck Programmcode, und dieser Code wurde
bisher in deinem Browser uebersetzt, bevor das erste Bild stand - jedes Mal
aufs Neue, rund 28.000 Zeilen. Gemessen auf dieser Maschine: **22,2 Sekunden**.
Dazu kam eine 2,7-Megabyte-Hilfsbibliothek, die dafuer erst geladen und
ausgepackt werden musste.

**Jetzt wird einmal beim Bauen uebersetzt.** Das Ergebnis liegt fertig bei, die
Hilfsbibliothek wird gar nicht mehr geholt. Dieselbe Messung: **63
Millisekunden**. Die Seite selbst schrumpft von 1,86 Megabyte auf 109 Kilobyte.
Wer eine aeltere Fassung von Hand veraendert, verliert nichts - Qwirbel merkt
das an einem Fingerabdruck und nimmt dann wieder den alten, langsamen Weg,
statt etwas Falsches anzuzeigen.

**Beim Umbau sind sieben echte Fehler aufgefallen, die vorher niemand sehen
konnte.** Der alte Uebersetzer hat sie zugedeckt: Werte, auf die zugegriffen
wurde, bevor es sie gab, wurden stillschweigend zu "nichts". Der teuerste davon:
Qwirbel hielt eine laufende Bilderzeugung nie fuer beschaeftigt und durfte die
Oberflaeche mitten hinein neu laden. Kein Absturz, keine Meldung - nur ein
Verhalten, das sich niemand erklaeren konnte. Eine Pruefung faengt solche
Stellen ab jetzt dauerhaft ab.

**"Meine Chats sind weg" - waren sie nie.** Waehrend der Verlauf vom Server
kam, zeigte der Chat den Willkommens-Schirm. Das sieht nicht aus wie "laedt
gerade", sondern wie "alles verloren", und nichts sprach dagegen. Jetzt steht
dort, dass geladen wird - und dass nichts verloren geht. Dauert irgendetwas
anderes laenger als einen Augenblick, laeuft oben ein schmaler Streifen.

**Der Ordner, den du gesetzt hast, gilt jetzt auch.** Wer einen Arbeitsordner
angibt, erwartet, dass Qwirbel dort arbeitet und dort sucht. Im Auftragstext an
die KI stand aber nur das WORT "Arbeitsordner" - ohne den Pfad. Das Modell
suchte folgerichtig in den Ordnern, die es kannte: Home, Schreibtisch,
Arbeitsbereich. Jetzt steht der echte Pfad dort, an allen drei Stellen, an
denen Qwirbel mit der KI redet. Bis Rechte-Stufe 7 ist er die Vorgabe - auch
fuers Suchen. Auf Stufe 8 (alles erlaubt) darf die KI darueber hinaus, wenn die
Aufgabe es verlangt.

**Neu: schlicht oder vollstaendig.** Unter Darstellung waehlst du, wie du durch
Qwirbel navigierst - die neue Kopfleiste (vorne Chat und Work, dahinter was
gerade laeuft) oder die gewohnte Seitenleiste mit allen Reitern. Es
verschwindet nichts, nur der Weg dorthin ist ein anderer. Der Reiter, in dem du
gerade steckst, steht dabei immer vorne.

**Untertabs lassen sich anheften.** Rechtsklick auf einen Unterpunkt zeigt sein
Zeichen, seinen Namen und das Tastenkuerzel - und "Als Haupt setzen". Danach
oeffnet der Hauptreiter immer genau diesen Unterpunkt. Modelle oeffnet
ab jetzt von sich aus die Modellbibliothek statt der Liste des bereits
Installierten: wer noch nichts hat, stand dort vor einer leeren Liste.

**Empfohlen werden jetzt Modelle, mit denen man wirklich arbeiten kann.**
Bisher schlug Qwirbel dichte Modelle vor, die ihre volle Groesse rechnen
muessen. Neu sind quantisierte Experten-Modelle: gemma-4-26B traegt 26
Milliarden Parameter an Wissen, rechnet aber nur mit vier davon je Wort - und
passt mit 9,8 Gigabyte auf dieselbe Karte wie ein deutlich duemmeres Modell.
Fuer kleinere Karten gilt dasselbe eine Nummer kleiner. Geladen wird nichts von
allein; der Vorschlag steht mit Groesse, Begruendung und einer ehrlichen
Antwort darauf, ob er auf DEINE Karte passt.

**Beim Einrichten wirst du gefragt, womit Bilder entstehen sollen** - mit dem
eingebauten Klecks oder mit ComfyUI, oder mit beidem. Qwirbel schaut vorher
nach, was wirklich da ist. Und weil sich so etwas aendert, kommt die Frage nach
jedem Update genau einmal wieder.

**Und du kannst sehen, wo Qwirbel seine Sachen ablegt.** Unter Einstellungen →
Dateien & Speicher steht jeder Ordner mit Groesse, Zweck und - das ist der
Punkt - was ein Loeschen kosten wuerde. Die Chats haben keine zweite Kopie; die
Modelle sind nur wiederbeschaffbar. Wer das nicht sehen will, schaltet es am
Ende des Setups ab; geloescht oder abgeschaltet wird dabei nichts.

**Die Oberflaeche kann jetzt jede Sprache lernen.** Unter Einstellungen →
Sprache legst du mit einem Plus eine neue an, und ein Modell uebersetzt die
2.433 Texte des Programms - in Abschnitten, mit sichtbarem Fortschritt, und
jederzeit anzuhalten. Was schon uebersetzt ist, bleibt gespeichert. Ehrlich
dazu: rund 540 Stellen setzen ihren Text erst beim Anzeigen zusammen ("Ich sehe
16 GB") - die bleiben auf Deutsch oder Englisch, ebenso alles noch nicht
Uebersetzte. Die Oberflaeche bleibt dadurch immer bedienbar.

**Kleinere Fehler:** Im Modell-Menue blieb die Ollama-Liste stumm leer, wenn
Ollama nicht lief - jetzt steht dort, woran es liegt. Und wer nur Klecks
benutzt, bekam statt der Modellwahl einen Setup-Knopf angeboten.

## v2.8.6 - Die Sprache wird gemessen statt geraten, und Klecks sieht endlich alle Modelle

**Beim ersten Start stand die Sprache falsch – auf einem deutschen Windows.**
Das ist der Fehler, der eine Fassung nach seiner eigenen Behebung wieder
aufgetaucht ist, nur von der anderen Seite. In v2.8.5 liest Qwirbel die Sprache
des Systems – und das tut es richtig: unter Windows die Anzeigesprache des
Benutzerkontos. Das FENSTER fragte aber jemand anderen. Es nahm die Sprache der
Browser-Laufzeit, die in dem eingebauten Fenster steckt, und die meldet oft
Englisch, auch wenn Windows deutsch ist. Im Einrichtungs-Assistenten war damit
der englische Knopf vorausgewaehlt – und ein markierter Knopf sieht aus wie
*das ist deins*. Wer darauf klickte, hatte sein Qwirbel auf Englisch gestellt,
ohne es zu wollen.

**Jetzt fragt das Fenster den Server.** Der weiss es, weil er das
Betriebssystem direkt fragen kann. Die Vermutung aus der Browser-Laufzeit gilt
nur noch fuer den Sekundenbruchteil, bis die richtige Antwort da ist. Und wer
einmal selbst eine Sprache gewaehlt hat, behaelt sie – korrigiert wird nur die
Vorbelegung, nie die Entscheidung.

**Klecks sieht jetzt alle Modelle, die da sind.** Bisher las er ausschliesslich
seine eigenen Ordner. Das war richtig gedacht – er soll ohne Ollama
funktionieren, und das tut er weiterhin. Nur: wer Ollama installiert hat und
sich dort ein Modell holt, sah es bei Klecks nicht. Jetzt gilt beides. Klecks
eigene Ordner bleiben die Grundlage; was Ollama zusaetzlich hat, kommt dazu.
Dieselbe Datei unter zwei Namen erscheint dabei nur EINMAL – Qwirbel erkennt
das an der Datei selbst, nicht am Namen.

**Und der Modelle-Tab zeigt es.** Bisher standen dort die Modelle von Ollama,
ComfyUI und den anderen Quellen – Klecks fehlte, obwohl er rechnet. Jetzt ist
er dabei, mitsamt der Angabe, ob ein Modell auf die Grafikkarte passt. Weil die
Abfrage bei Klecks ein paar Sekunden dauert, wird sie kurz zwischengespeichert;
wie frisch die Liste ist, steht mit dabei. Eine stille alte Zahl waere genau
die Art Anzeige, die spaeter wie ein Fehler aussieht.

**Klecks laedt jetzt das Modell, das du gewaehlt hast.** Zwei Beschwerden,
eine Ursache: *"Er tut da einfach ein anderes laden, was dann nicht antwortet"*
und *"Der Prompt hat 10303 Marken, das Fenster fasst 8192."* Dahinter stand
eine einzige falsch gelesene Angabe. Qwirbel fragte Klecks *laeufst du?* und
verstand die Antwort als *ist ein Modell geladen?* - gemeint war aber *liegen
brauchbare Modelldateien da?*. Weil immer welche dalagen, kam Qwirbel nie zum
Laden: das zuletzt benutzte Modell blieb auf der Karte, egal was oben im Chip
stand, und dessen Textfenster war zu klein fuer die Anfrage.

**Jetzt gilt, was im Chip steht.** Liegt ein anderes Modell auf der Karte, wird
gewechselt. Ist das Textfenster zu klein, wird es mit dem groesseren neu
geladen, statt dir vorzurechnen, wie viele Marken fehlen. Bei dieser Art
Rechenwerk steht die Fenstergroesse beim Start fest - Ollama macht deshalb
genau dasselbe, nur unsichtbar. Und wenn das Laden wirklich scheitert, sagt
Qwirbel das weiterhin klar, mit Modellname und Zahl.

**Die Modell-Liste im Chip haelt sich auf dem Laufenden.** Sie wurde bisher
einmal geholt und blieb dann stehen. Wer im Klecks-Tab alle Modelle sah und
oben im Chip nur drei, hatte genau das vor sich. Jetzt merkt Qwirbel, wenn sich
die Zahl der verfuegbaren Modelle aendert - weil ein Dienst neu startete oder
eine Datei dazukam - und holt die Liste dann nach. Nicht dauernd: die Abfrage
kostet ein paar Sekunden, und alle acht Sekunden waere sie teurer als ihr
Nutzen.

**Kleinigkeit mit grosser Wirkung:** Die Zustandsabfrage von Klecks wartete bei
jedem Aufruf zwei Sekunden darauf, dass auf einem geschlossenen Anschluss
niemand antwortet. Jetzt fragt sie erst kurz nach, ob dort ueberhaupt jemand
ist. Dieselbe Antwort, nur in einer Viertelsekunde statt in zwei.

**Was sich NICHT geaendert hat, und das ist Absicht:** Ollama bleibt der
Standard – im Programm und in der Einrichtung. ComfyUI bleibt fuer Bilder,
Video und Musik. Klecks laeuft daneben und wird sichtbar besser. Woran man
erkennt, wann er so weit ist, steht ab dieser Fassung als Liste mit Zahlen im
Programmordner (`KLECKS-BEREIT-KRITERIEN.md`): neun Schwellen, zwei davon
gruen. Solange auch nur eine rot ist, bleibt es beim bewaehrten Weg.

## v2.8.5 - Qwirbel antwortet in DEINER Sprache, und das Symbol holt das Fenster zurueck

**Zwei Kaeufer haben denselben Nachmittag zwei Fehler gemeldet, und beide waren
echt.** Der eine hatte sein Programm auf Englisch gestellt und bekam trotzdem
deutsche Antworten. Der andere schloss das Fenster mit dem X und kam danach nur
noch ueber den Browser hinein. Beides ist behoben – und in beiden Faellen war
die Ursache nicht das, wonach es aussah.

**Die Sprache: es waren zwei Regeln, die sich widersprochen haben.** Im
Grundtext, den Qwirbel jedem Modell mitgibt, stand fest verdrahtet *Antworte
IMMER auf Deutsch, ohne Ausnahme*. Bei englischer Einstellung wurde ans Ende
desselben Textes gehaengt *Answer exclusively in ENGLISH*. Das Modell bekam also
zwei Anweisungen, beide als wichtigste bezeichnet, und musste raten. Einer der
Kaeufer hat den Denkverlauf seines Modells mitgeschickt – darin dreht es sich
minutenlang im Kreis und schreibt woertlich *This is a conflict*. Er hatte recht.

**Jetzt kann Qwirbel jede Sprache, und der Standard ist die des Nutzers.**
Schreibt jemand franzoesisch, antwortet Qwirbel franzoesisch; wechselt er
mitten im Gespraech, wechselt Qwirbel mit. Wer eine feste Sprache will, waehlt
sie – dann gilt sie ueberall und ohne Ausnahme, in achtundzwanzig Sprachen von
Deutsch und Englisch ueber Franzoesisch, Spanisch, Portugiesisch, Tuerkisch,
Polnisch bis Japanisch. Die Regel selbst steht jetzt an EINER Stelle im
Programm statt an vier, und ein Test faellt durch, sobald wieder zwei
verschiedene Sprachen in einem Text landen.

**Das Desktop-Symbol holt das Fenster zurueck.** Das X schliesst nur das
Fenster – Qwirbel laeuft danach im Hintergrund weiter, das ist Absicht. Wer
dann das Symbol doppelt anklickte, bekam aber nur einen Hinweis, er moege das
vorhandene Fenster benutzen oder das Symbol im Infobereich anklicken. Nur: das
Fenster gab es nicht mehr, und Windows blendet Symbole im Infobereich
standardmaessig aus. Man sah einen Zettel, fand nichts und ging in den Browser.
Jetzt sieht Qwirbel nach, ob ueberhaupt ein Fenster da ist – und macht eins auf,
wenn keins da ist. Genau das, was ein Doppelklick tun soll.

**Das Setup sagt jetzt, was es tut.** Bisher hiess das Fenster immer *Setup*,
auch wenn laengst eine Fassung installiert war. Jetzt steht dort *Update*, wenn
eine aeltere gefunden wird, *Reparieren* bei derselben – und *Aeltere Fassung*,
wenn man versehentlich eine aeltere EXE ueber eine neuere Installation legt.
Der letzte Fall ist der Grund fuer die Unterscheidung: eine Rueckstufung soll
man lesen koennen, bevor man auf Weiter drueckt.

**Der Update-Kanal holt je System das richtige Paket.** Qwirbel gibt es sechsmal
– Windows, Linux und macOS, jeweils als Normal- und als Server-Fassung. Das
Update-Manifest kannte aber nur EINE Adresse fuer alle. Jetzt steht dort je
System und Variante ein eigener Eintrag, und Qwirbel nimmt den, der zu diesem
Rechner passt. Findet er keinen, laedt er NICHTS – ein Windows-Paket auf einem
Mac auszupacken waere schlimmer als gar kein Update. Aeltere Manifeste
funktionieren unveraendert weiter.

**Qwirbel misst jetzt selbst, was in deinem Rechner steckt.** Die
Modell-Empfehlung fragte bisher ausschliesslich ComfyUI nach der Grafikkarte –
auf einem Rechner ohne ComfyUI kam schlicht nichts heraus, und die
Selbst-Einrichtung blieb wirkungslos. Jetzt liest Qwirbel die Karte selbst, aus
mehreren Quellen je nach System, und sagt bei jeder Zahl dazu, woher sie stammt.
Findet er keine Karte, sagt er das – statt einen Wert zu raten.

**Und die Empfehlungen selbst hatten Loecher.** Zwischen den Stufen klafften
Luecken: eine Karte mit 7,95 GB fiel durch alle Stufen hindurch in einen
Rueckfall, der ausgerechnet die groesste Empfehlung war – ein Modell mit
knapp 20 GB auf einer 8-GB-Karte. Jetzt sind die Stufen lueckenlos, der
Rueckfall ist die kleinste statt der groessten, und es gibt eigene Stufen fuer
Rechner ohne Grafikkarte, fuer 4 GB und fuer 24 GB aufwaerts. Apple Silicon
wird als das behandelt, was es ist: gemeinsamer Speicher, keine getrennte Karte.

**Die Motoranzeige unten links hat die Unwahrheit gesagt** – und zwar genau
verkehrt herum. Sie meldete *rechnet*, sobald irgendeine Modelldatei auf der
Platte lag, und *bereit* ausgerechnet dann, wenn keine da war. Jetzt
unterscheidet sie, ob ein Modell geladen ist, ob nur welche herumliegen, ob ein
Teil im Hauptspeicher liegt (dann ist es spuerbar langsamer, und das steht
jetzt da) – und ob die Antwort schlicht nicht rechtzeitig kam. Der letzte Fall
ist ein eigener Zustand: keine Antwort heisst nicht *aus*, sondern *unklar*.

**Fuer Firmen: eine Rechte-Luecke ist geschlossen.** Fuenf Werkzeuge, mit denen
Qwirbel auf einem verbundenen Zweitgeraet Dateien lesen und schreiben kann,
waren fuer Mitarbeiter-Konten nicht gesperrt – und die Geraeteliste filtert
nicht nach Mandant. Ein Mitarbeiter haette damit jedes angemeldete Geraet
erreichen koennen, auch das der Geschaeftsfuehrung. Bis es eine Zuordnung von
Geraeten zu Konten gibt, sind diese Werkzeuge fuer Mitarbeiter gesperrt.

**Kleinigkeiten, die im Alltag auffallen:** Ein Modell laesst sich jetzt direkt
in Klecks eigenen Ordner laden, mit Fortschritt und Abbrechen – bisher landete
jeder Download im Ordner des anderen Motors, der ihn nie zu sehen bekam. Die
Modell-Liste im Chat-Menue fuellt sich nach, wenn Klecks spaeter gestartet wird,
statt bis zum naechsten Neustart leer zu bleiben. Und die Zustandsabfrage des
Rechenwerks braucht statt zwei Sekunden nur noch eine Viertelsekunde: sie
wartete jedes Mal darauf, dass auf einem geschlossenen Anschluss niemand
antwortet.

## v2.8.4 - Qwirbel spricht die Sprache deines Rechners

**Auf einem englischen Windows war bisher alles deutsch.** Ein Kaeufer meldete
es genau so: sein System ist englisch, sein Qwirbel war es nicht. Das lag nicht
an einer Einstellung, die er uebersehen hatte – es war schlicht fest verdrahtet.
Ohne gespeicherte Wahl fiel die Oberflaeche auf Deutsch zurueck, und der
Setup-Assistent kannte ueberhaupt keine zweite Sprache: das allererste, was ein
englischer Kunde von Qwirbel zu sehen bekam, war ein Fenster, das er nicht lesen
konnte.

**Jetzt entscheidet der Rechner.** Beim ersten Start liest Qwirbel die Sprache
des Systems – unter Windows die Anzeigesprache des Benutzerkontos, sonst die
ueblichen Sprach-Einstellungen. Deutsch bleibt Deutsch, alles andere wird
Englisch. Wer in den Einstellungen selbst etwas waehlt, ueberstimmt das
dauerhaft; die eigene Wahl gewinnt immer. Auch die Sprache, in der Qwirbel
ANTWORTET, folgt beim ersten Start dem System statt einer festen Vorgabe.

**Das Setup-Fenster gibt es jetzt auf Englisch.** Vollstaendig: Schritte,
Erklaerungen, Knoepfe, die Beschreibung jeder Variante, jede der zwoelf
Datengruppen bei der Uebernahme, die Lizenz-Texte, die Warnungen bei
Fehleingaben. Auch die Konsolen-Ausgabe, die man zu sehen bekommt, wenn das
Fenster nicht startet. Was noch keine Uebersetzung hat, erscheint unveraendert
auf Deutsch statt zu verschwinden – eine fehlende Zeile ist ein Schoenheits-
fehler, eine verschluckte waere ein Fehler.

**Und ein Test passt ab jetzt darauf auf:** er zaehlt jeden sichtbaren Text im
Setup-Fenster und faellt durch, sobald einer ohne Uebersetzung dasteht. Beim
Bauen dieser Fassung waren das 45 Texte im Fenster plus 30 aus den Varianten-
und Datengruppen-Listen – alle uebersetzt.

**Fuer wen sich nichts aendert:** wer Qwirbel schon benutzt, behaelt seine
Sprache. Die Erkennung greift nur, wo noch nie etwas gewaehlt wurde.

## v2.8.3 - ONTOGO: Der Schwarm-Check feuert jetzt wirklich

**Die Setup-EXE verlangt keine ZIP mehr.** Ein Kaeufer meldete: Doppelklick auf
`Qwirbel-Setup.exe`, und statt zu installieren fragt das Fenster nach einer
Programm-ZIP - obwohl das Programm in der EXE steckt. Das war ein echter Fehler,
und er betraf **jede** Setup-EXE bis einschliesslich v2.8.1, Normal wie Server.

Beim Verpacken landete das Programm-Paket in einem Unterordner statt in der
Wurzel der EXE. Das Setup sucht es an der richtigen Stelle, fand dort nichts und
fiel deshalb auf die letzte Notloesung zurueck: den Nutzer nach der ZIP fragen.
Auf dem Entwicklungsrechner ist das nie aufgefallen, weil dort neben der EXE
immer das Release-ZIP liegt - der Rueckfall hat es gefunden, und alles sah
gesund aus. Genau das ist die Lehre: **eine Setup-EXE muss in einem leeren
Ordner getestet werden, sonst prueft man die eigene Festplatte statt das
Produkt.**

Behoben, und zwar gemessen: die neuen EXEs tragen das Paket in der Wurzel, und
beide Varianten wurden allein in einem leeren Ordner durchlaufen - Normal wie
Server installieren ohne eine einzige Rueckfrage. Dazu ein Test, der genau das
festnagelt: er prueft den Bau-Aufruf, das Verhalten bei falsch abgelegtem Paket
und die fertigen EXEs auf dem Datentraeger.

**Zweiter Fund im selben Zug:** Die Notloesung „ZIP neben der EXE" suchte nur
nach Normal-Paketen. Ein Server-Kaeufer haette also selbst diesen Rueckweg nicht
gehabt. Sie kennt jetzt beide Varianten, und die Fehlermeldung sagt auch, welche
Datei sie eigentlich sucht.

**Wer betroffen war und was zu tun ist:** Wer per ZIP installiert hat, war nie
betroffen. Wer eine Setup-EXE bis v2.8.1 hat, nimmt einfach die neue - oder legt
die Programm-ZIP neben die alte EXE, dann laeuft auch die durch. Auf dem Rechner
bleibt in beiden Faellen nichts Halbes zurueck: das Setup bricht ab, bevor es
etwas anfasst.

**Der automatische Schwarm-Start („großes Projekt → aufteilen“) feuerte nie – zwei Tore
blockierten ihn.** Erstens verlangte _grosses_projekt zwingend eine Roadmap-Datei im
Projektordner: Fehlte sie, kam immer „klein“ heraus, egal wie riesig der Auftrag war –
deshalb startete der Auto-Schwarm nie von allein. Jetzt gilt: Roadmap ODER Nachricht ab
300 Zeichen, die mehrere Dinge auf einmal nennt. Die KI denkt dabei weiterhin erst
selbst nach: Die Zerlegung läuft über das LLM, ergibt sie nur EINEN Teil, arbeitet der
Agent allein weiter – eine bewusste Entscheidung MIT oder OHNE Schwarm, ohne Rückfrage
(genau Falkos Wunsch: „du denkst erst mal nach“).

**Zweitens warf ein mitgeschicktes Bild die Nachricht aus dem Aufgaben-Weg.** Ein Bild
erzwang vorher überall typ=generation – auch im Work-/Code-Tab. Damit verschwand die
Nachricht in der Bild-Pipeline, BEVOR der Schwarm-Check sie überhaupt sah; eine „große
Nachricht mit Bild in einen neuen Code-Tab“ konnte den Schwarm-Check deshalb nie
erreichen. Jetzt ist ein Bild in Work/Code KONTEXT für die Aufgabe (die Vision-
Beschreibung wandert in die Aufgaben-Nachricht), nur ein explizit gewählter Workflow-
Chip bleibt Generation – im Chat-Tab wie bisher.

**User-Zwischennachrichten erscheinen genau einmal.** Das Echo eines Zurufs konnte
mehrfach ankommen (Reload/Reconnect spielt Events nach) – die Nachricht stand dann zwei-
oder dreimal im Chat. zwischenrufEcho ist jetzt idempotent: Existiert bereits ein
bestätigter Zwischenruf mit demselben Text, fliegt nur die vorläufige Zeile raus,
eingefügt wird nichts mehr. Dasselbe Netz jetzt auch an der SENDEN-Stelle: Schickt Falko
dieselbe Nachricht mehrfach los (Doppelklick, Enter + Klick), meldet das Backend
"duplikat" und die vorläufige Zeile verschwindet wieder, statt doppelt stehen zu
bleiben. Und der Verlaufs-Schreiber verwirft ein zweites identisches Zwischenruf-Echo –
quittieren mehrere Helfer denselben Posteingang (Broadcast UND Stream), landet die Zeile
trotzdem nur einmal in der Chat-Datei. Nur FALKOS Zwischenrufe werden entdupliziert;
Qwirbels eigene Meldungen bleiben unberührt.

## v2.8.2 - Kleine Modelle wissen jetzt, was sie schon getan haben

**Ein Modell unter 34 Milliarden Parametern bekommt nach jedem Befehl eine
Ansage im Klartext.** Der Befund kam aus dem laufenden Betrieb: ein Gemma im
Work-Tab hatte mehrere Werkzeuge ausgefuehrt - ein Python-Skript geschrieben,
Workflows konvertiert - und wollte danach trotzdem wieder bei null anfangen,
weil es sein eigenes Ergebnis nicht als "fertig" gelesen hat. Grosse Modelle
sehen das rohe Werkzeug-Ergebnis und verstehen es; kleine brauchen es gesagt.
Ab jetzt steht nach jedem Zug eine Zeile in ihrem Verlauf: welches Werkzeug
lief, mit welchen Angaben, was dabei herauskam - und der ausdrueckliche Satz,
dass genau dieser Befehl NICHT noch einmal auszufuehren ist. Bei einem
Fehlschlag steht ebenso deutlich da, dass nichts bewirkt wurde und eine
blinde Wiederholung nichts aendert.

**Diese Ansage bleibt im Kontext stehen.** Sie ist angeheftet: muss der
Verlauf gekuerzt werden, faellt sie nicht als Erstes weg, sondern bleibt Wort
fuer Wort - gerade kleine Modelle haben das kleinste Fenster und brauchen sie
am dringendsten. Damit das Anheften das Fenster nicht selbst sprengt, bleiben
die juengsten zwoelf Ansagen fest; aeltere stehen weiter lesbar da und duerfen
mitgekuerzt werden.

**Wer sie nicht bekommt:** Modelle ab 34 Milliarden Parametern, die grossen
Cloud-Modelle - und die Kommunikations-Werkzeuge (melden, nachfragen, Plan
aendern, weiterplanen). Bei denen waere "fuehr das nicht nochmal aus" genau
verkehrt herum, die duerfen sich wiederholen. Laesst sich die Groesse eines
lokalen Modells nicht feststellen, gibt es die Ansage lieber: sie kostet ein
paar Marken, ihr Fehlen kostet doppelte Arbeit. Abschaltbar ueber
agent.werkzeug_echo, die Schwelle steht in agent.werkzeug_echo_ab_b.

**Die Browser-Bruecke laesst nur noch deine eigene Erweiterung herein — und
deine Erweiterung nur noch deinen eigenen Qwirbel.** Bisher galt: wer sich
beim Anklopfen als Browser-Erweiterung ausgab, war drin. Fuer eine Webseite
ist das tatsaechlich eine Huerde, die sie nicht nehmen kann. Fuer ein
Programm auf demselben Rechner ist es keine: drei Zeilen Code genuegen, um
sich als Erweiterung auszugeben — und damit haette es deinen Browser samt
aller offenen Anmeldungen fernsteuern koennen.

Jetzt bekommt die Erweiterung beim ersten Verbinden ein Dauer-Token, und
Qwirbel merkt sich, welche Erweiterung das war. Danach kommt nur noch diese
eine durch: falsches Token, fremde Kennung oder gar keins — abgewiesen, und
der Versuch wird mitgeschrieben. Abtippen musst du dafuer weiterhin nichts.

**Und die Erweiterung glaubt jetzt nicht mehr jedem, der am anderen Ende
antwortet.** Beim Verbinden schickt sie eine Zufallszahl und verlangt eine
Signatur damit zurueck — die kann nur bilden, wer das Token kennt. Kommt sie
nicht oder ist sie falsch, macht die Erweiterung die Verbindung zu und
fuehrt **keinen einzigen Befehl** aus. Vorher haette jedes Programm, das
schneller auf dem Port sitzt, ihr Befehle geben koennen.

**Neu koppeln geht ueber den Knopf, den es schon gibt:** Einstellungen →
Verbindung → Browser koppeln. Der oeffnet fuer fuenf Minuten ein Fenster,
in dem sich eine Erweiterung anmelden darf, und liefert wie bisher zusaetzlich
einen Code. Wer es ganz streng mag, stellt `browser_bruecke.streng` an —
dann koppelt sich nichts mehr von selbst, auch nicht beim ersten Mal.

⚠️ **Nach diesem Update die Erweiterung einmal neu laden** (in
chrome://extensions der Kreis-Pfeil auf ihrer Karte). Sie verbindet sich
danach von selbst und holt sich dabei ihr Token.

**Der Update-Knopf fragt jetzt wirklich jemanden.** „Jetzt pruefen" im
Updates-Tab meldete bisher „Kein Manifest konfiguriert" - es gab die ganze
Update-Maschinerie (Kanaele, gestaffelter Rollout, Pruefsummen, Rollback), aber
keine Adresse, an die sie sich haette wenden koennen. Ab jetzt fragt jede
Installation von selbst bei Qwirbels oeffentlicher Info-Seite auf GitHub nach:
Version, was neu ist, fuer welchen Kanal freigegeben. Ist etwas Neues da, sagt
Qwirbel es - mit den Stichpunkten aus der neuen Fassung.

**Und wenn ein Paket bereitsteht, gibt es einen Knopf dafuer.** „Jetzt
installieren" laedt es, prueft die Pruefsumme und wendet es an; die Sicherung
davor macht Qwirbel wie immer selbst. Passt die Pruefsumme nicht, wird nichts
angewendet - dann steht lieber die alte Fassung da als eine halbe neue. Der
Neustart bleibt ein eigener Klick, damit ein Update keine laufende Aufgabe
mitreisst. Steht kein Paket zum Direkt-Laden bereit, erscheint auch kein Knopf,
sondern die Bezugsquelle - ein Knopf, der beim Druecken erklaert, warum er
nicht geht, ist schlimmer als keiner.

**Eine leere Update-Adresse heisst ab jetzt „nicht eingetragen", nicht „aus".**
Das klingt nach Kleinkram und war der eigentliche Fehler: die Adresse als
Standard im Programm zu hinterlegen reichte nicht, weil in JEDER gespeicherten
Einstellungsdatei bereits ein leerer Wert stand - und der gewinnt gegen einen
Standard. Bestandsinstallationen haetten den Knopf also weiterhin fuer kaputt
gehalten. Wer den Update-Kanal wirklich nicht will, traegt jetzt ausdruecklich
„aus" ein; Firmen koennen wie bisher auf ihr eigenes Manifest zeigen.

**Die Leiste ganz links ist wieder durchsichtig.** Seit v2.8.0 ist das eigene
Hintergrundbild eine eigene Ebene und keine der Hintergrund-Wahlen mehr. Die
Seitenleiste hatte ihre Glas-Optik aber genau an diese alte Wahl gehaengt -
also stand sie bei Sternenhimmel, Aurora, Nebel, Wellen und Raster wieder als
deckende Saeule neben einem laufenden Hintergrund. Sie nimmt jetzt dieselbe
Lasur wie die Kopfzeile oben, bei jedem Hintergrund. Nur die Schublade in der
Handy-Ansicht bleibt deckend: die liegt ueber dem Inhalt, dort waere
durchsichtig unlesbar.

## v2.8.1 - Klecks laedt, was er zeigt

**Die Klecks-Modellliste und ihr Lade-Knopf sprechen wieder ueber denselben
Motor.** Klecks hat zwei Rechenwege: sein eigenes Vulkan-Rechenwerk und den
llama-server als Massstab und Rueckfall. Die Liste im Klecks-Tab zeigte seit
dem Motor-Umbau die Modelle des eigenen Rechenwerks - der Lade-Knopf pruefte
aber weiter gegen den Katalog des llama-servers. Ergebnis: drei Modelle im
Menue, und jedes davon brachte beim Klick "Modell kenne ich nicht. Vorhanden:"
mit dreizehn fremden Namen dahinter. Jetzt gehen Anzeigen, Laden und Entladen
ueber denselben Motor. Gemessen nach dem Fix: Qwen3-4B liegt gut fuenf
Sekunden nach dem Klick auf der Karte, die Gegenprobe (als geladen markiert,
VRAM wirklich belegt) stimmt, und Entladen raeumt es nachweisbar wieder weg.

**VRAM FREIGEBEN wirft jetzt auch Klecks' Chatmodell raus.** Der Knopf unten
links kannte Ollama, Colibri und ComfyUI - lief Klecks als eigener Dienst
daneben, blieb sein Modell einfach liegen, und keine Meldung nannte es. Jetzt
wird es mit entladen, steht namentlich in der Erfolgsmeldung und zaehlt in
der freigeraeumten Zahl mit. Gemessen: 2,3 GB geworfen, 13,6 GB frei danach.

**Klecks startet jetzt auch auf Linux und macOS.** Bisher gab es nur die
START.bat fuer Windows. Jetzt liegen START.sh (Linux) und "START (Mac).command"
(Doppelklick auf dem Mac) daneben - dieselbe dreistufige Python-Wahl wie
unter Windows: erst die ausdrueckliche Wahl aus klecks.json, dann Klecks'
eigene Umgebung, zuletzt das System-Python mit ehrlicher Ansage. Eine
Wahrheit, drei Tueren.

**Die Seitenleiste laesst sich am PC einklappen - der Pfeil oben links.**
Wer viele Dinge gleichzeitig offen hat - Agenten, Auftraege, mehrere Chats,
Plaene - dessen Seitenleiste wird lang, und bei einer Vorfuehrung soll der
Inhalt die Buehne haben. Ein Klick auf den Pfeil neben dem Logo klappt
alles auf die schmale Icon-Leiste zusammen, wie man es vom Handy kennt;
ein zweiter Klick holt alles zurueck. Die Wahl bleibt gespeichert, auch
ueber einen Neustart.

**Klecks liegt jedem Paket bei - und als eigener Download.** Jedes der sechs
Qwirbel-Pakete (Windows, Linux, macOS, jeweils Normal und Server) traegt
Klecks ab jetzt als Unterordner; Qwirbel findet ihn dort von allein. Wer nur
Klecks will, nimmt die neue Klecks-Universal-ZIP: ein einziger Download, der
auf allen drei Systemen startet. Die Rechenwerke (llama.cpp) und die Modelle
sind bewusst nicht enthalten - zusammen weit ueber 200 MB, und beides haengt
an der eigenen Hardware. Klecks holt sich beide beim ersten Start selbst.

## v2.8.0 - Zwei Bibliotheken, Hochskalieren und ein Sternenhimmel

**Deine eigenen Modell-Ordner werden endlich wieder gefunden.** Wer eine
GGUF-Datei in seinen Modell-Ordner legte, sah sie unter Models danach
trotzdem nirgends - und Ollama kannte sie auch nicht. Der Grund war ein
einziger Eintrag: Qwirbel schaute nur in EINEN Ordner, und wenn der aus den
Einstellungen verschwand, suchte er stillschweigend in einem leeren
Standard-Ordner weiter. Ohne Fehlermeldung, ohne Hinweis. Jetzt durchsucht
Qwirbel ALLE Modell-Ordner - den eingestellten, den Standard-Ordner und den
Ordner neben Ollamas eigenem Speicher. Und unter Models -> Eigene Dateien
steht jetzt schwarz auf weiss, WO gesucht wurde, samt Feld zum Umstellen.
Ein leerer Ordner sieht damit nicht mehr aus wie ein kaputtes Programm.
Wichtig bleibt: eine GGUF-Datei im Ordner ist fuer Ollama noch kein Modell -
dafuer gibt es den Knopf "In Ollama importieren" direkt daneben.

**Aus dem Store wird die Modellbibliothek - mit allem an einem Ort.** Die
kuratierten Familien und die grosse Hugging-Face-Liste standen bisher in zwei
getrennten Untertabs; man musste wissen, dass es beides gibt. Jetzt ist es ein
Tab: oben die Familien mit Beschreibung, und wer weiterscrollt, landet
nahtlos in der vollstaendigen Liste aller Modelle, die schreiben koennen.

**Aus der ComfyUI-Basis wird die Generationsbibliothek - und die zeigt
endlich, was ein Workflow wirklich braucht.** Vorher war das eine flache
Liste von Dateinamen. Jetzt klappst du einen Workflow auf und siehst jedes
Modell, das er braucht, mit seiner Aufgabe: das grosse Bild- oder
Video-Modell, den Text-Encoder, die VAE, die LoRAs, den Hochskalierer. Klappst
du eines davon auf, siehst du JEDE Fassung, die es davon auf Hugging Face
gibt - alle GGUF-Stufen, fp8, bf16 - jeweils mit Groesse, einer Einschaetzung
zu Qualitaet und Tempo und einem ehrlichen Satz dazu: was du gewinnst, was du
verlierst, ob es auf deine Karte passt und dass du eine kleinere Stufe mit ein
paar Schritten mehr wieder aufholen kannst. Eine Fassung traegt die
Empfehlung: die groesste, die auf deiner Karte noch bequem laeuft.

**Deutlich mehr zum Generieren.** Die Bibliothek kennt jetzt 14 Workflows
statt 9 - fuenf lagen schon im Ordner, tauchten aber nirgends auf: zwei
Kurz-Clips in 480p und 720p, eine schnelle Video-Variante und zwei Wege,
Bewegung aus einem Referenzvideo auf eine eigene Figur zu uebertragen. Dazu
ein zweiter Teil im selben Tab, sortiert nach Familie: Z-Image, Qwen-Image und
Qwen-Image-Edit, FLUX.1, Chroma, Stable Diffusion 3.5 und SDXL, HiDream,
Lumina, WAN 2.1 und 2.2 samt Animate und VACE, HunyuanVideo, LTX-2.3 und
ACE-Step fuer Musik. 46 Modell-Plaetze aus 37 geprueften Quellen, jeder mit
allen Fassungen zum Aufklappen. Geladen wird ausschliesslich aus genau diesen
geprueften Quellen - kein beliebiger Download-Weg.

**Der Tab sagt jetzt die Wahrheit, auch wenn ComfyUI aus ist.** Bisher fragte
Qwirbel die laufende ComfyUI, welche Modelle sie kennt. War sie aus, galt
schlagartig alles als "fehlt" - auch die Modelle, die seit Wochen auf der
Platte liegen. Jetzt schaut Qwirbel selbst nach, in jedem Ordner, den ComfyUI
benutzt (auch auf externen Platten). Nebeneffekt: der Tab oeffnet in rund zwei
Sekunden statt in vierzehn, weil dieselbe Abfrage nicht mehr dreimal
hintereinander laeuft.

**Hochskalieren ist jetzt eine eigene Funktion – im Chat und als Knopf.**
Wer Comfy und Klecks im Haus hat, soll fuer ein groesseres Bild nicht zu Topaz
gehen muessen. Sag es einfach: „skalier das Bild hoch" oder „mach das Video
groesser" – Qwirbel nimmt den passenden Hochskalierer, rechnet und legt das
Ergebnis in den Chat. Unten in der Chat-Zeile steht dazu ein Knopf: Faktor 2x,
3x oder 4x waehlen, Modell waehlen (oder Qwirbel entscheiden lassen) und die
angehaengten Bilder loslegen. Bis zu zehn Bilder auf einmal – sie laufen
NACHEINANDER durch, weil es nur einen Platz auf der Grafikkarte gibt; parallel
waeren alle langsamer. Videos gehen auch: jedes Einzelbild laeuft durch
dasselbe Modell, die Tonspur bleibt erhalten. Qwirbel sagt vorher, dass es
dauert, statt es hinterher zu erklaeren. Und er nimmt nie einen Hochskalierer,
der nur zu einem bestimmten Video-Modell gehoert – aus einem Foto wuerde damit
Matsch.

**Mehr Hintergruende, und die Sterne bewegen sich.** Zu Deko, Schlicht,
Maskottchen und eigenem Bild kommen fuenf neue: **Sternenhimmel** (driftende
Sterne, ab und zu eine Sternschnuppe), **Aurora** (weiche Farbschleier),
**Nebel** (ruhig atmende Schwaden), **Wellen** (drei Lagen, die langsam
durchziehen) und **Raster** (Gitter mit Horizont). Alle nehmen deine
Akzentfarbe auf, alle stehen beim FPS-Regler still wie die Deko, und wer
Bewegung im System abgestellt hat, bekommt dasselbe Bild – nur ruhig. Auch per
Zuruf: „mach mir einen Sternenhimmel" im Darstellungs-Tab reicht.

**Dein eigenes Bild geht jetzt ZUSAMMEN mit den Animationen.** Bisher war
„eigenes Bild/Video" eine der Hintergrund-Optionen – entweder dein Foto oder
Sterne, nie beides. Jetzt ist es ein zweiter, eigener Schalter: oben waehlst du
die Basis (Sterne, Aurora, Nebel, Wellen, Raster, Deko, Schlicht, Maskottchen),
darunter haakst du „Eigenes Bild/Video zusaetzlich" an – dein Foto liegt dann
unten, die Animation darueber. Wer vorher „eigenes Bild" eingestellt hatte,
sieht genau dasselbe wie vorher; die Einstellung wird beim ersten Oeffnen
still umgestellt. Auch per Zuruf: „mein Foto mit Sternen darueber".

**Kleinkram:** Passt eine Fassung nicht auf die Karte, steht das als Satz
darunter statt als stiller Haken. Steht ComfyUI still, wird der
Grafikspeicher aus dem eingestellten VRAM-Profil genommen statt "unbekannt"
zu melden. Laufende Downloads ueberleben ein Neuladen der Seite. Die alten
Untertab-Namen fuehren weiter an die richtige Stelle, falls sie irgendwo
verlinkt sind. Und zwei Workflows, die viel Grafikspeicher brauchen, warnen
jetzt vorher statt hinterher zu enttaeuschen.

## v2.7.8 - Löschen löscht wirklich, Qwirbeln schließt sauber, lokale Modelle arbeiten

**Der Lösch-Knopf löscht jetzt WIRKLICH.** Bisher stand beim Löschen „es geht
nichts verloren, wird nur verschoben“ – der Chat wanderte als .alt.jsonl zur
Seite und blieb damit auf der Platte liegen. Falko: „Der Knopf soll aber halt
löschen. den Chat, den man dann hat.“ Der Knopf schickt jetzt hart:true und das
Backend entfernt die Chat-Datei wirklich (unlink) – schnell, ohne LLM-Runde;
die Anbieter-Bindung des Kanals löst sich mit (ein neuer Chat wählt neu). /neu
und Qwirbeln archivieren weiterhin wie gehabt – nur der Lösch-Knopf löscht.

**Das Qwirbeln-Fortschrittsfenster schließt nach Abschluss sicher.** Es konnte
hängen bleiben, wenn der Lauf ungewöhnlich endete – und danach war der Knopf
blockiert. Jetzt gibt es EINEN finally-Aufräumweg statt dreier if-Zweige: Wie
der Lauf auch ausgeht (Abweisung durchs Backend, normales Stream-Ende, Fehler),
wird der Auto-Reload freigegeben und das Fenster schließt nach 2,6 Sekunden –
der Knopf ist sofort wieder verwendbar, auch für den nächsten Chat. Endet der
Stream ohne Abschluss-Meldung (Backend-Neustart, Verbindungsabbruch), wird der
Lauf ehrlich beendet statt ewig „läuft“ zu zeigen – der Chat bleibt dabei
unangetastet stehen.

**Chat-Tab: funktioniert jetzt mit jedem Modell ab 25B Parametern – mit Tool
Calls, Web Search usw.** Die Werkzeug-Liste im Prompt ist kompakt und ohne
MCP-Ballast, dadurch greifen große lokale Modelle (wie Gemma 26B quantisiert
über Klecks) sicher zu: Werkzeug-Aufrufe, Websuche und Web-Lesen laufen im
Chat, statt dass das Modell an der Liste stolpert oder Sperrmeldungen kassiert.

**Work und Code: lokale Modelle arbeiten jetzt.** Dieselbe kompakte
Kern-Werkzeugliste (~18 sortierte Werkzeuge, 3,4 KB statt 52 KB Prompt), die den
Chat-Tab schnell gemacht hat, gilt jetzt auch in Work und Code: Lokale Modelle
unter 30B sehen nur die Kern-Liste und arbeiten damit sicher; Cloud-Modelle und
große lokale Modelle (ab 30B) behalten die volle Liste wie bisher.

## v2.7.7 - Jeder Chat bleibt bei seinem Modell

**In Work und Code bindet der erste Zug den Chat an seinen Anbieter – lokal ODER
Cloud.** Der Zwang vom 21.08. („Arbeits-Tabs nur noch lokale Modelle“) blockierte
dort jeden API-Key und war der Back, weswegen dieses Update nie installiert wurde.
Jetzt gilt: Startet Falko einen Work-/Code-Chat mit GLM, bleibt genau dieses Modell
für den gesamten Chat gesetzt – die Modell-Leiste wirkt „grau“, ein stiller Wechsel
findet nie statt. Lokal bindet sofort; Cloud bindet nur mit passendem Key (ohne Key
kommt ein ehrlicher Fehler mit Grund und Ausweg, kein stiller Rückfall auf lokal).
Ein neuer Chat (qwirbeln/leeren) wählt neu. Chat, Planung und Mind bleiben frei –
dort gilt die Leiste wie bisher. Die Entscheidung steht als EINE Wahrheit in der
neuen Datei backend/chat_fixierung.py (wahl_fuer_chat), nicht mehr als if-Blöcke
an zwei Stellen in main.py.

**Gemma 26B arbeitet jetzt auch in Work/Code – mit der kompakten Werkzeugliste.**
Falkos Gemma 4 26B lief im Chat-Tab schnell und sicher, weil die Werkzeug-Liste
kompakt war und kein MCP-Ballast im Prompt stand. Genau das gilt ab jetzt auch in
Work und Code: Die Schwelle für die vollständige ~60-Werkzeug-Liste steigt von 25
auf 30 Milliarden Parameter (werkzeug_profile.VOLL_AB_B_DEFAULT=30) – Modelle
darunter sehen die sortierte Kern-Liste (~18 Werkzeuge, 3,4 KB statt 52 KB Prompt)
und greifen dadurch sicherer zu. Cloud-Modelle und große lokale Modelle (ab 30B)
behalten die volle Liste wie bisher.

**Der MCP-Chip ist aus der Promptbox entfernt.** Er zeigte in Work und Code „null“
und verwirrte mehr, als er half. Der Chat läuft ohne zugeschaltete MCP-Werkzeuge
(wer sie will, aktiviert sie in den Einstellungen; mcp.auto_im_chat bleibt aus).

**Mühe- und Rechte-Regler gelten jetzt pro Tab.** Der Berechtigungs-Regler war
global: eine Stufe im Code-Tab stellte auch Chat, Work und Planung um. Jetzt hält
jeder Kanal seine eigene Stufe (qw_autonomie8_<kanal>), genauso wie der
Mühe-Regler daneben (qw_muehe8_<kanal>).

**Während Falko spielt, darf Qwirbel ins Fenster schauen.** fenster_ansehen ist
bewusst nicht mehr in der Vollbild-Sperre – Reinschauen reißt ihn nicht aus dem
Spiel. Eigene Fenster und Programme gehören auf den anderen Monitor; die
Sperrmeldung nennt beides wörtlich als Ausweg.

**Klecks läuft jetzt in jedem Chat-Zweig.** Die Chat-Zweige riefen hart Ollama auf –
der Chip „Klecks (eigene Engine)“ wurde ignoriert. EINE Wahrheit wie im Agent-Loop:
_lokal_chat_gen fragt lokale_llm, wer rechnet (Ollama streamt echt, Klecks liefert
die fertige Antwort als einen Zug).

## v2.7.6 - Wer lokal will, wird gehoert

**Im Chat antwortet ab jetzt genau der Anbieter, der ausgewaehlt ist.** Bisher
baute Qwirbel sich bei leerer Ausweich-Reihenfolge selbst eine: gewaehlter
Anbieter zuerst, danach alle anderen aktivierten. Aus der Wahl "Gemini" wurde
so die Reihe Gemini, Anthropic, z.ai und zwei weitere - ein Schluckauf beim
ersten, und geantwortet hat der zweite. Fuer eine laufende Aufgabe ist dieser
Rueckfall richtig und bleibt auch so; sie soll nicht an einem kurzen
Serverfehler sterben. Fuer eine Chat-Antwort ist er falsch, denn dort ist die
Modellwahl eine Ansage. Antwortet der Gewaehlte nicht, kommt jetzt ein
ehrlicher Fehler statt einer Antwort aus einem fremden Haus.

**Klecks galt im Chat nicht als lokale Wahl.** Die Pruefung "will der Nutzer
lokal arbeiten" kannte ollama, aber nicht klecks. Damit kam die Wahl als
"unbekannt" beim Lade-Tor an und wurde mit dem Hinweis auf die aktiven
API-Schluessel abgewiesen - daher war bei ausgewaehltem Klecks von fremden
Anbietern die Rede, obwohl dorthin nie etwas ging.

**Und das Lade-Tor sagt endlich, wen es abgewiesen hat.** Es schuetzt die
Grafikkarte davor, dass ein Modell ungefragt hineingeladen wird - eine
richtige und weiterhin gueltige Regel. Im Protokoll stand aber nur, DASS
abgewiesen wurde. Bei ueber hundert Absagen an einem Tag liess sich daraus
nicht bestimmen, welche der 49 Stellen im Programm gefragt hatte, an denen ein
lokales Modell laufen kann; die Suche nach "warum will da eine API antworten"
wurde zur Archaeologie. Jetzt steht die aufrufende Stelle mit Datei und Zeile
daneben. Ein Tor, das nicht sagt, wen es abweist, ist nur ein halbes
Protokoll.

## v2.7.5 - Im Chat gilt, was ausgewaehlt ist

**Wer im Chat Gemini auswaehlt, bekam manchmal eine Antwort von Anthropic.**
Nicht als Fehler, sondern als eingebaute Hilfsbereitschaft: faellt ein
Anbieter aus, geht der naechste in der Reihe weiter. Steht keine eigene
Reihenfolge in den Einstellungen, baut Qwirbel sie selbst - und haengt dafuer
alle aktivierten Cloud-Anbieter hintereinander. An einer echten Konfiguration
gemessen wurde aus der Wahl "Gemini" die Reihe Gemini, Anthropic, z.ai und
zwei weitere. Ein einziger Schluckauf beim ersten, und geantwortet hat der
zweite. Fuer eine LAUFENDE Aufgabe ist das genau richtig - sie soll nicht an
einem kurzen Serverfehler sterben, und der Wechsel wird dort auch angezeigt.
Fuer eine Chat-Antwort ist es falsch: dort ist die Modellwahl eine Ansage und
kein Vorschlag. Im Chat wird ab jetzt genau der gewaehlte Anbieter gefragt.
Antwortet er nicht, kommt ein ehrlicher Fehler statt einer Antwort aus einem
fremden Haus. Work und Code behalten den Rueckfall unveraendert.

**Ausserdem war bei ausgewaehltem Klecks von Anthropic die Rede, obwohl
dorthin gar nichts ging.** Der Chat pruefte, ob der Nutzer lokal arbeiten
will - und diese Pruefung kannte "ollama", aber nicht "klecks". Klecks
galt damit als Cloud-Anbieter, die Wahl kam als "unbekannt" beim Lade-Tor
an, und das sperrte mit dem Hinweis auf die aktiven API-Schluessel. Es war
also nie ein Aufruf in die Cloud, sondern eine Fehlmeldung ueber einen - was
es nicht besser macht, nur schwerer zu finden. Klecks zaehlt jetzt als das,
was es ist: der lokale Motor.

## v2.7.4 - Zurufe kommen zurueck, und der Chat kann sparen

**Wer mitten in der Arbeit etwas zuruft, konnte es nie zuruecknehmen.** Ging ein
Zwischenruf raus und der Satz war doch noch nicht fertig, lief er trotzdem: Der
Agent las ihn beim naechsten Zug, egal was. Jetzt ist die eigene, noch unter-
wegs Blase klickbar - ein Klick nimmt die Nachricht aus dem Posteingang des
Agenten, sie verschwindet aus dem Chat und der Text liegt wieder in der
Eingabe zum Bearbeiten. Hat der Agent sie schon gelesen, ist der Klick weg und
eine ehrliche Meldung sagt, dass es zu spaet ist. Gleichzeitig antwortet er auf
Zurufe ernsthafter: Substanz (Ergebnis, Entscheidung, naechster Schritt) statt
den Nutzersatz nachzuplappern.

**Und der Chat hat einen Spar-Hahn.** Im Modell-Chip gibt es bei API-Modellen
jetzt einen Token-Sparmodus: Ist er an, schickt Qwirbel je Anfrage nur noch die
Haelfte des Verlaufs mit (6 statt 12 Nachrichten, 3000 statt 6000 Zeichen) - der
wiederholte Praefix ist bei Cloud-Chats der groesste Token-Posten, und genau der
laesst sich so je Anfrage fast halbieren. Der Knopf steht nur bei Cloud-Modellen,
wo Tokens Geld kosten; lokal aendert sich nichts, und aus bleibt aus: Ohne den
Knopf bleibt alles exakt wie vorher.

**Dazu drei stille Reparaturen:** Der "hat nichts getan - fasse nach"-Nudge
feuert nicht mehr im Chat (ein Chat-Zug ohne Werkzeug ist dort die NORMALE
finale Antwort, keine behauptete Aktion). Das Fenster-Schloss ist jetzt GLOBAL -
Werkstatt und Installation blockieren sich gegenseitig, statt zwei Fenster mit
zwei Tray-Icons zu oeffnen. Und der Packer laesst fuenf Repo-Reste (Diagnose-
und Schwarm-JSONs, Google-Snapshot, Babel-Check) draussen, die nie in ein
Paket gehoerten.

## v2.7.3 - Der Empfindlichkeits-Regler hat jetzt Luft nach oben

**Das Diktat hatte eine unsichtbare Decke.** Der Regler fuer die Empfindlichkeit
des Live-Diktats liess sich bislang bis 5 stellen - und genau dort stand er bei
Falko schon lange. Wer leiser sprach oder ein Stueck weiter vom Mikro sass,
wurde schlicht nicht mehr erkannt; Drehen half nichts, denn die Skala hinter
dem Regler endete bei 5 und klemmte jeden hoeheren Wert stumm dorthin zurueck.
Ab jetzt reicht der Regler bis 10, und die Erkennung nutzt den ganzen Weg:
Stufe 10 nimmt auch leise, weiter entfernte Sprache noch an. Der alte Schutz
bleibt dabei unangetastet - die Schwelle liegt weiterhin IMMER ueber dem
gemessenen Grundrauschen, nur dichter darunter (Faktor 1,04 statt 1,08), damit
das Diktat nicht anfaengt, Geraetebrummen mitzuschreiben. Und es bleibt eine
reine Einstell-Sache: Nichts an der Diktat-Architektur wurde geaendert, nur
die Skala darueber wurde erweitert.

**Gemessen statt behauptet:** Die Diktat-Suite prueft jetzt 64 Faelle (vorher
47), inklusive der neuen Stufen 7,5 und 10, und bleibt komplett gruen. Die
volle Regression ueber alle 102 Suiten lief am 21.08. mit 102 gruennen und
null roten durch. Wer bisher auf Stufe 5 stand, dreht einfach weiter nach
rechts - sein Wert bleibt erhalten, es kommt nur Spanne dazu.

## v2.7.2 - Er weiss wieder, was vorher war

**"Fix mir das" hatte bisher kein "das".** Wer im Work- oder Code-Tab einen
Auftrag gibt, dann das Ergebnis sieht und sagt "mach da noch was dran",
bekam einen Agenten, der bei null anfaengt. Der Grund war unscheinbar: der
Weg, ueber den ein Auftrag startet, hat dem Agenten den bisherigen Verlauf
nie mitgegeben. Er baut sich seinen Kontext aus dem Auftragssatz, dem Ziel
und einer frischen Erkundung des Projektordners - und das war alles. Der
Verlauf lag die ganze Zeit auf der Platte, mit jedem Satz und jeder
Werkzeug-Zeile darin. Er wurde nur nie zurueckgegeben. Ab jetzt bekommt
jeder Auftrag das, was in seinem Chat schon passiert ist: was gewuenscht
war, was Qwirbel selbst dazu notiert hat, welche Dateien er wirklich
veraendert hat und was er zuletzt geantwortet hat. Bewusst schmal - reines
Lesen bleibt draussen, das steht im Lese-Gedaechtnis darunter und zaehlt
sonst zweimal aufs Budget. Und bewusst als eigener Baustein statt an einer
einzelnen Stelle verdrahtet: so gilt es fuer den Chat, fuer bestaetigte
Plaene, fuer die Automatik und fuer Schwarm-Helfer gleichermassen.

**Dieselbe Datei wurde bis zu 72-mal gelesen, weil das Gedaechtnis sich
selbst ueberschrieben hat.** Seit dem letzten Update behaelt Qwirbel, was
er gelesen hat. Der Schluessel dafuer war aber nur "Werkzeug plus Pfad" -
ohne die Stelle. Damit teilten sich "Zeilen 1 bis 100 dieser Datei" und
"Zeilen 900 bis 1000 derselben Datei" einen einzigen Eintrag, und der
zweite Zugriff warf den ersten weg. Brauchte er den Anfang wieder, musste
er ihn erneut oeffnen. Genau die Schleife, die eigentlich beendet werden
sollte. An echten Protokollen nachgezaehlt: 1165 gespeicherte Inhalte sind
so vernichtet worden, das ist jeder fuenfte Lesevorgang. In einer einzigen
Sitzung teilten sich 72 verschiedene Lesungen derselben grossen Datei einen
Eintrag, bei zwei weiteren Dateien waren es 40 und 35. Jetzt gehoert die
Eingrenzung in den Schluessel - Zeilenbereich, Suchbegriff, Suchmuster.
Dieselbe Stelle ein zweites Mal gelesen ersetzt den Eintrag weiterhin, denn
die Datei kann sich geaendert haben. Eine ANDERE Stelle loescht die vorige
nicht mehr.

**Was ueber MCP gelesen wurde, kam als Stummel an.** Die eigenen
Lese-Werkzeuge duerfen bis zu vierzehntausend Zeichen ins Gedaechtnis
schreiben. Ein Datei-Werkzeug ueber MCP stand in dieser Tabelle nicht und
bekam deshalb den Standardwert: neunhundert Zeichen. Im Gedaechtnis landete
also ein Anfang statt eines Inhalts, und beim naechsten Mal wurde dieselbe
Datei wieder geoeffnet. Die Buchhaltung dafuer war schon repariert worden,
die Obergrenze nicht. Lesende MCP-Werkzeuge bekommen jetzt dieselbe Grenze
wie die eigenen; schreibende bleiben knapp, dort ist die Ausgabe ohnehin
kurz.

**Der Zaehler zeigte 566, das Modell bekam 304.100.** Beide Zahlen waren
richtig, sie massen nur Verschiedenes. Die Anzeige zaehlte die Chat-Datei -
und darin steht je Werkzeug-Aufruf eine Zeile von rund neunzig Zeichen. Was
tatsaechlich an das Modell geht, ist etwas anderes: die Werkzeug-Doku, die
Doku der zugeschalteten MCP-Server, das Lese-Gedaechtnis und der Verlauf,
und zwar bei jedem einzelnen Zug neu. An einer echten Installation
gemessen sind das rund neununddreissigtausend Marken Sockel, bevor der
Auftrag ueberhaupt beginnt. Der Kopf-Platz zeigt jetzt diesen Wert, und die
Aufteilung im Tooltip kommt aus denselben Funktionen, aus denen der Prompt
gebaut wird - nicht aus einer Schaetzung im Browser, die von Werkzeug-Doku
und Lese-Gedaechtnis gar nichts wissen konnte. Deshalb stand dort bisher
"hundert Prozent Nachrichten, null Prozent Dateien". Gerechnet wird das
je Reiter, nicht einmal fuer alle: der Chat bekommt eine kleinere
Werkzeug-Liste als Work und Code, und MCP-Server nur, wenn man sie dort
ausdruecklich zuschaltet. Im Chat stehen deshalb rund viertausend Marken,
wo im Code-Tab knapp dreissigtausend stehen - vorher zeigten beide
dieselbe grosse Zahl.

**Daneben steht jetzt, was der Chat wirklich gekostet hat.** Der Balken
zeigt einen Fuellstand - wie voll der Kopf gerade ist. Das ist etwas
anderes als die Summe ueber das ganze Gespraech, und man kann das eine
nicht aus dem anderen ausrechnen. Also gibt es beides: neben dem Balken die
gezogenen Marken dieses Chats, im Tooltip zusaetzlich, wie viel davon aus
dem Prompt-Cache kam. Diese zweite Zahl ist der eigentliche Punkt. Eine
grosse Summe klingt teuer, ist es aber nicht, wenn fast alles ein
Cache-Treffer war: in einer Messung waren es 103.400 gezogene Marken, davon
97.500 aus dem Cache - frisch bezahlt wurden 5.900. Ohne diese Zeile waere
die grosse Zahl nur ein Schreckgespenst. Beim Qwirbeln faengt der Zaehler
bei null an.

**Der eigene PC hielt sich nach jedem Neuladen fuer ein fremdes Geraet.**
Startet man einen Auftrag und drueckt danach F5, stand da "Laeuft auf einem
anderen Geraet" - auf genau der Maschine, die den Auftrag gestartet hat.
Die Geraete-Kennung wurde bei jedem Seitenaufbau neu gewuerfelt, sie
konnte einen Neustart also gar nicht ueberleben. Sie haengt jetzt am Geraet
statt an der Seite und ueberlebt Neuladen, Fenster-Neustart und
Backend-Neustart. Steht die Meldung zu Recht da, weil wirklich ein anderes
Geraet arbeitet, sieht man dort ausserdem, wie lange es schon laeuft und
was gerade getan wird - vorher stand dort nur der Satz und sonst nichts.

**Klecks galt an drei Stellen noch als Cloud-Dienst.** Klecks ist der
lokale Motor, aber an mehreren Stellen wurde nicht gefragt "ist das lokal",
sondern "heisst das ollama". Fuer das Kontext-Budget hatte das Folgen: ein
Klecks-Modell bekam ein Budget nach einem geratenen Fenster von 32.768
Marken zugeteilt, waehrend der Dienst das Modell mit deutlich weniger
geladen hatte. Ein Budget, das groesser ist als das Fenster, ist genau der
Weg, auf dem der Anfang eines Gespraechs still herausfaellt. Ausserdem
uebersprang die Groessen-Pruefung fuer Modelle jedes Klecks-Modell
komplett - dort war die Frage ebenfalls falsch gestellt.

**Ein Modellwechsel konnte den Anfang wegwerfen, ohne es zu sagen.** Es gab
bereits eine Pruefung, ob der laufende Verlauf ueberhaupt in das Fenster
des gewaehlten Modells passt. Sie sah aber nur den Gespraechs-Ausschnitt,
den der Aufrufer mitschickte - und bei einem bestaetigten Plan, in der
Automatik oder bei einem Schwarm-Helfer kommt gar keiner mit. Dann entfiel
die Pruefung stillschweigend. Gemessen wird jetzt, was der Tab wirklich
umfasst. Passt es nicht, kommt eine Ansage mit beiden Zahlen und dem
Unterschied zwischen "das Modell kann nicht mehr" und "Qwirbel laedt es
kleiner" - samt dem naheliegenden Ausweg: qwirbeln.

**Kleinigkeiten, die man taeglich sieht.** Beim Zeigen auf eine Anzeige
erschien unter dem dunklen Qwirbel-Tooltip zusaetzlich das graue Kaestchen
des Browsers, mit unaufgeloesten Platzhaltern darin. Es wurde zwar
unterdrueckt, aber die Oberflaeche schrieb es bei jeder Aktualisierung
zurueck - und der Token-Zaehler aktualisiert im Sekundentakt. Jetzt bleibt
es weg, und der eigene Tooltip laeuft dabei live mit. Ausserdem: ein
bestaetigter Plan, der ueber die Programmierschnittstelle gestartet wird,
gab den Chat nicht mit weiter - sein Lese-Gedaechtnis landete im falschen
Chat und war dort nicht wiederzufinden.

## v2.7.1 - Was Qwirbel gelesen hat, vergisst er nicht mehr

**Er hat dieselben Dateien immer wieder gelesen, und der Grund war ein
Gedaechtnis, das mit dem Auftrag stirbt.** Waehrend eines Auftrags merkt
sich Qwirbel, was er schon gelesen hat - das gab es bereits. Nur lebte
dieses Wissen ausschliesslich im Arbeitsspeicher des laufenden Auftrags.
Beim naechsten Auftrag im selben Chat stand er wieder ohne Inhalte da,
sah eine Datei, die er eigentlich kannte, und las sie neu. Danach las er
darin einzelne Zeilen nach, weil auch die weg waren.

**Es gab schon einen Merkzettel, aber er war absichtlich duenn.** Er hielt
fest, WELCHE Dateien der Chat kennt - mit Groesse, Aenderungszeit und
etwa vierhundert Zeichen Auszug. Bewusst kein Inhalt, damit der Kontext
nicht zulaeuft. Das war eine vertretbare Abwaegung und hat sich in der
Praxis nicht bewaehrt: er wusste, WO etwas steht, aber nicht WAS - also
musste er trotzdem nochmal hinsehen. Ab jetzt bleibt der Inhalt
erhalten, in einer eigenen Datei je Chat, mit Obergrenzen nach oben (eine
grosse Datei je Quelle, insgesamt einige Megabyte je Chat - danach faellt
das Aelteste heraus).

**Wichtig ist, was das NICHT bedeutet:** der Chat schickt deshalb nicht
mehr Text an das Modell. Was tatsaechlich mitgegeben wird, entscheidet
weiterhin das Kontext-Budget des jeweiligen Modells. Der Speicher ist
gross, die Auswahl daraus bleibt klein - und genau das ist der Punkt: ein
grosses Cloud-Modell bekommt mehr davon zu sehen als ein kleines lokales,
aber keines von beiden muss die Datei ein zweites Mal oeffnen.

**Beim Qwirbeln wird alles ausgewertet und weggeraeumt** - Merkzettel und
Inhalte zusammen. Ein frischer Chat faengt sauber an und traegt nicht die
Lektuere des alten mit sich herum.

**Ausserdem: neun GLM-Modelle statt vier.** Am Endpunkt nachgefragt - z.ai
bietet neun an, die Liste im Programm kannte vier. Gemessen an glm-5.3:
erreichbar, rund 55 Marken je Sekunde, Werkzeug-Aufrufe funktionieren
sauber. Es denkt allerdings viel; bei einer Ein-Satz-Frage gingen 398 von
483 Marken ins Denken. Deshalb bekommt dieser Anbieter bewusst keine enge
Marken-Grenze - sonst landet die ganze Antwort im Denk-Block und beim
Nutzer kommt eine leere Blase an.

## v2.7.0 - Er sieht seine Werkzeuge, benutzt mehrere auf einmal und redet dabei mit

**Von 138 zugeschalteten Werkzeugen kannte Qwirbel nur 40.** Die anderen
98 standen nicht im Prompt - 19 nur als Name ohne Argumente, 79 kamen
ueberhaupt nicht vor. Fuer ein Modell besteht zwischen "dieses Werkzeug
gibt es nicht" und "ich muss danach fragen" genau dieser eine Unterschied.
Gesperrt waren sie nie: ein Aufruf ging immer durch, es fehlte allein das
Wissen um den Namen. Man sah das in den Protokollen - Playwright-Werkzeuge
wurden neunmal gerufen, obwohl sie nirgends standen; das Modell hatte die
Namen aus seinem Weltwissen geraten. Bei einem Server mit eigenen
Bezeichnungen geht das nicht. Jetzt stehen alle mit Aufrufform und
Beschreibung da. Die Sorge, das wuerde die Suche erschweren, hat sich am
lebenden Modell ins Gegenteil gedreht: dieselbe Aufgabe, die vorher nach
fuenf Minuten ohne Ergebnis endete, war mit vollstaendiger Liste nach 27
Sekunden richtig beantwortet. Wer nicht sucht, ist schneller.

**Nebenbei ist ein Fehler aufgefallen, der jeden fuenften Werkzeug-Aufruf
kostete.** In der Doku stehen Typangaben in spitzen Klammern - und
Modelle setzten die woertlich als Wert ein. Einundzwanzig Aufrufe in den
Protokollen scheiterten so. Dass diese Klammern keine Werte sind, stand
bis jetzt nirgends.

**Roblox Studio laesst sich jetzt wirklich steuern.** Qwirbel startete
dafuer ein fremdes Paket aus dem Netz, das reproduzierbar mit
"Connection closed" abbrach - es wartet auf ein Zusatzprogramm im Studio,
das es gar nicht gibt. Dabei liefert Roblox seinen eigenen Server mit,
direkt im Programmordner. Genau den nimmt Qwirbel jetzt: Skripte lesen
und aendern, den Spielbaum durchsuchen, das Spiel starten und stoppen,
die Konsole mitlesen. Das ist kein Sonderfall fuer Roblox, sondern ein
Weg fuer jedes Programm, das einen solchen Server mitbringt - eintragen
laesst sich das mit zwei Zeilen. Die Sicherheitsschranke bleibt dabei zu:
in der Einstellung steht kein Pfad, sondern ein Schluessel, und den Pfad
sucht Qwirbel selbst an einer festen Stelle. Eine von Hand eingetragene
Programmdatei bleibt genauso verboten wie vorher.

**Mehrere Werkzeuge in einem Zug.** Drei Dinge, die nichts voneinander
wissen - zwei Dateien lesen und den Git-Stand zeigen - kosteten bisher
drei volle Denkrunden. Die Werkzeuge selbst brauchen Millisekunden, das
Nachdenken davor je nach Modell zehn Sekunden bis mehrere Minuten. Wer
die Reihenfolge vertauschen kann, ohne dass sich am Ergebnis etwas
aendert, darf sie jetzt zusammen schicken. Sobald ein Aufruf auf die
Antwort eines anderen wartet, bleiben es zwei Runden - das ist der
Unterschied, und er steht so im Prompt. Geht einer davon schief, werden
die uebrigen verworfen statt blind weitergefahren. Jeder einzelne Aufruf
laeuft dabei durch dieselben Sperren wie vorher; es gibt keinen zweiten
Weg an ihnen vorbei.

**Und er sagt beim Arbeiten, was er gerade herausgefunden hat.** Bisher
ging das nur ueber ein eigenes Werkzeug - und das kostete jedes Mal eine
komplette Denkrunde. In den Protokollen stehen ueber siebenhundert
solcher Zuege, die nichts gebaut haben. Jetzt faehrt der Satz beim
Werkzeug mit und kostet nichts extra.

**Das Kontextfenster stellt sich selbst.** Es stand fest auf 16384 -
fuer jedes Modell dasselbe. Gemessen an einer echten Installation war das
mal zufaellig richtig und mal weit daneben: ein Modell, das 131072 Token
haelt, lief auf einem Achtel davon. Eine groessere feste Zahl waere
genauso falsch gewesen, denn neben einem grossen Modell ist auf der
Grafikkarte kein Platz fuer ein grosses Fenster - es wuerde auf den
Hauptprozessor auslagern und langsamer statt besser. Jetzt wird
gerechnet: was das Modell kann, was neben ihm in die Karte passt, und
davon der kleinere Wert. Kleiner als bisher wird es nie. Wer aus gutem
Grund bremsen will, kann das weiterhin von Hand. Bei Anbietern ueber
einen Schluessel galt diese Grenze ohnehin nie - dort bringt der Anbieter
sein Fenster mit.

**Der Verlauf zeigt jetzt, was wirklich passiert ist.** Von den
Werkzeug-Schritten wurde nur ein Fuenftel gespeichert; vier Fuenftel
fielen lautlos weg. Nicht nur Nachlesen - auch Dateien loeschen, Python
ausfuehren, mehrere Stellen auf einmal aendern standen nicht in der
Liste. Der eigentliche Fehler war, dass es eine Abschlussliste war: was
nicht daraufstand, verschwand, und ein neues Werkzeug fiel automatisch
heraus. Jetzt kommt jeder Schritt an, und aufeinanderfolgende Schritte
klappen sich zu einer Zeile zusammen - so wie waehrend der Arbeit.

**Was er nicht pruefen kann, aendert er nicht mehr einfach.** Bisher
stand an dieser Stelle sinngemaess: bau ruhig, du kannst es hier zwar
nicht testen, sag es im Schlussbericht. Das ist die falsche Reihenfolge.
Kann Qwirbel nicht hinsehen, ob eine Aenderung wirkt, sagt er das jetzt
sofort und sorgt zuerst dafuer, dass er hinsehen kann. Neue Dateien
anlegen bleibt in Ordnung - die kann man wegwerfen. Bestehende
umschreiben nicht. Und ein Werkzeug, das nicht verbindet, ist ab jetzt
die Aufgabe und keine Fussnote: er geht dem Grund nach, statt es einmal
zu versuchen und nie wieder.

**Dazu gibt es einen Rueckweg.** Bevor eine bestehende Datei zum ersten
Mal in einer Aufgabe geaendert wird, legt Qwirbel eine Kopie daneben -
einmal je Datei, nicht bei jedem Aufruf. Wo eine Versionsverwaltung
laeuft, unterbleibt das, dort gibt es den Weg zurueck schon.

**Kleine Auftraege bekommen keinen Werkstattbericht mehr.** Die Tabelle
am Ende war fuer jede Groesse bestellt - auch fuer "lies mir diese Datei
vor". Gemessen kam mehr als ein Drittel der Auftraege mit hoechstens drei
Werkzeug-Aufrufen aus. Dafuer gibt es jetzt zwei bis drei Saetze. Ab
vier Aufrufen bleibt alles wie gehabt.

**Und die Zwischennachrichten haben keinen Pfeil mehr.** Der gehoerte nie
dorthin - er ist fuer die Werkzeugliste da, die sich aufklappen laesst.

## v2.6.9 - Die Figuren bewegen sich jetzt auch auf schnellen Bildschirmen

**Wer mehr als 60 Bilder je Sekunde eingestellt hat, sah keine einzige
Animation - und wusste nicht, warum.** Qwirbel kennt einen Sparmodus fuer
hohe Bildraten. Der ist sinnvoll: teure Effekte wie Weichzeichner oder
wandernde Flaechen kosten dort wirklich Leistung. Nur waren die neuen
Figuren mit in dieser Abschaltung gelandet, obwohl sie fast nichts
kosten - ein paar Rechtecke, die sich verschieben. Das Ergebnis war ein
merkwuerdiges Bild: der Knopf der hoechsten Stufe leuchtete weiter, weil
er als Einziger nicht in der Liste stand, die Figuren daneben standen
still. Jetzt laufen sie auch dort, nur ruhiger - laengere Zyklen, keine
Funken. Ganz still wird es erst in der ausdruecklichen Spar-Stufe ab 165
Hertz, und natuerlich weiterhin, wenn im Betriebssystem weniger Bewegung
gewuenscht ist. Das ist eine Ansage des Menschen und keine
Bildraten-Einstellung.

## v2.6.8 - Der Token-Zaehler sagt die Wahrheit

**Er hat gelogen, und zwar sichtbar.** Wer den Chat neu geladen hat, sah
die Token-Zahl fallen - als waere plotzlich die Haelfte des Gespraechs
verschwunden. War sie nicht. Der Zaehler holt sich die echte Zahl vom
Programm, das die Chat-Datei auf der Platte misst. Aber es gab nur EINEN
solchen Wert fuer ALLE Tabs gleichzeitig, und die Tabs bleiben im
Hintergrund geoeffnet. Wer zuletzt gezeichnet wurde, bestimmte, fuer
welchen Tab der Wert galt - alle anderen fielen auf eine Schaetzung
zurueck, die nur die gerade angezeigten Nachrichten kennt. Nach einem
Neuladen sind das weniger, also sank die Zahl. Jetzt hat jeder Tab
seinen eigenen Wert, und ein Takt fragt sie alle ab. Nach dem Loeschen
eines Chats wird sofort neu gemessen statt bis zu funfzehn Sekunden zu
warten - sonst sieht es aus, als haette das Loeschen nicht gewirkt.

**Und er passt wieder in die Leiste.** In Work und Code stehen mehr
Knoepfe als im Chat, und der neue Zaehler war breiter als der alte
Balken - er schob das Ende der Leiste aus dem Bild. Jetzt gibt er bei
wenig Platz zuerst das Beiwerk auf: erst die Angabe "noch frei", dann
die aufklappenden Anteile. Ring und Prozent bleiben immer stehen, denn
das ist die Aussage.

**Muehe und Rechte haben jetzt verschiedene Figuren.** Sie messen auch
verschiedene Dinge. Muehe ist Anstrengung: die Figur arbeitet sich hoch,
vom Sitzen bis zum Rennen. Rechte ist Vertrauen: dort geht es nicht um
Kraft, sondern darum, wie weit der Schild sinkt. Auf Stufe 1 steht die
Figur ganz dahinter und fragt bei allem nach, auf Stufe 8 hat sie ihn
abgelegt und die Arme offen.

**Die Figuren bewegen sich jetzt auch wirklich.** Sie taten es vorher
schon - nur um weniger als einen Bildschirmpunkt, weil die Wege im
falschen Massstab gerechnet waren. Aus einer Bewegung, die man nicht
sehen konnte, ist eine geworden, die man sieht, ohne dass sie zappelt.
Dafuer ist die Animation auf dem Knopf der hoechsten Stufe ruhiger
geworden: dort lagen drei Effekte uebereinander - ein wanderndes
Pixelraster, ein Lichtstreifen und ein schneller Puls. Das war Unruhe
ohne Aussage. Geblieben ist ein ruhiges Leuchten.

## v2.6.7 - Ein Maennchen, das zeigt, wie viel Muehe sich Qwirbel gibt

**Die acht Stufen haben jetzt ein Gesicht.** Wie viel Muehe sich Qwirbel
in einem Tab gibt und wie viele Rechte er ohne Rueckfrage hat - das waren
bisher zwei Zahlen von 1 bis 8. Zahlen sagen einem nichts, solange man
sie nicht gelernt hat. Jetzt steht neben jeder Stufe eine kleine
Pixelfigur, und die sagt es sofort: bei 1 und 2 sitzt sie mit
geschlossenen Augen da, ab 3 steht sie und schaut, ab 6 arbeitet sie mit
erhobenen Armen, und bei 8 rennt sie mit einer Aura und kleinen Funken.
Darunter laeuft eine Leiste aus acht Bloecken mit, die sich beim
Darueberfahren weich fuellt.

**Wichtig war uns dabei, wie es sich bewegt.** Eine Figur, die in
Einzelbildern zappelt, sieht nach kaputtem GIF aus und macht auf Dauer
nervoes. Deshalb rattert hier nichts: die Figuren atmen in ruhigen
Zyklen von zwei bis dreieinhalb Sekunden, Kopf und Koerper leicht
versetzt, damit es lebendig statt maschinell wirkt. Wer Animationen im
System abgeschaltet hat oder den Sparmodus nutzt, sieht sie ruhig
stehen - alles laeuft ueber eine Stelle, die sich abschalten laesst.

**Der Token-Zaehler ist ein Ring geworden.** Bisher stand dort ein
flacher Balken und zwei Zahlen. Aber "wie voll ist der Kopf" ist ein
Anteil, und einen Anteil liest man als Kreis schneller als als Zahl. Der
Ring fuellt sich und wechselt dabei die Farbe - gruen, gelb, rot - und
daneben steht, wie viel noch frei ist. Faehrt man mit der Maus darueber,
klappen vier feine Saeulen auf und zeigen, wohin der Platz geht:
Nachrichten, Dateien, Werkzeuge, MCP. Im Ruhezustand bleibt die Leiste
still, denn ein blinkender Zaehler erzieht nur dazu, ihn zu ignorieren.

**Alles davon ist gezeichnet, nicht geladen.** Keine Bilddatei, kein
Zugriff ins Netz - die Figuren sind ein paar Rechtecke, die sich mit dem
Farbschema mitfaerben und beim Zoomen scharf bleiben.

## v2.6.6 - Die eigene Engine steht da, wo sie hingehoert

**Klecks ist lokal, und das Menue sagt es jetzt auch.** Bisher stand die
eigene KI-Engine im Modell-Menue ganz unten bei den Cloud-Anbietern -
neben Diensten, an die Text wirklich das Haus verlaesst. Das war falsch
und es hat verunsichert, zu Recht. Klecks rechnet auf der Grafikkarte im
eigenen Rechner, genau wie Ollama, und steht deshalb ab sofort oben
unter LOKAL. Die Ursache war eine alte Abkuerzung im Programm: an
mehreren Stellen wurde nach dem NAMEN "ollama" gefragt, wo eigentlich
"ist das lokal?" gemeint war. Wer damals einen zweiten lokalen Motor
dazustellte, landete zwangslaeufig bei der Cloud. Fuenf solche Stellen
sind jetzt korrigiert.

**Und die Modelle, die fuer eine Aufgabe zu klein sind, sind auch dort
gesperrt.** Bei Ollama war das laengst so: ein Modell, das den Work-Tab
nicht tragen kann, ist ausgegraut, mit dem Grund beim Drueberfahren.
Fuer die eigene Engine galt das nicht - dort war alles waehlbar, auch
das, was danach nur scheitert. Schlimmer noch: das Menue haette in einem
Fall gesperrt und der Server das Modell trotzdem genommen. Die Schranke
gehoert der Aufgabe und nicht dem Weg, also gilt sie jetzt fuer beide
Motoren gleich.

**Auto, Hybrid und CPU wirken auf den Motor, der wirklich laeuft.** Die
drei Knoepfe schrieben ihre Einstellung immer nach Ollama - wer die
eigene Engine gewaehlt hatte, stellte damit etwas ein, das den laufenden
Motor nicht betraf. Ein Schalter, der umspringt und nichts bewirkt, ist
schlimmer als gar keiner. Neu ist ausserdem, was "Auto" bei der eigenen
Engine bedeutet: sie rechnet vor dem Laden aus, wie viele Schichten
wirklich auf die Karte passen - Gewichte plus Kontext-Fenster plus
Rechenpuffer - und sagt es im Klartext, wenn es nicht ganz reicht.
Vorher hiess es dort nur "nimm halt weniger", ohne eine Zahl zu nennen.

**Der Loeschen-Knopf in den Chats funktioniert.** Ein geloeschter Chat
wurde auf der Platte korrekt archiviert, aber der Reiter blieb stehen -
und nach dem Neuladen war der Chat wieder da. Der Grund: die Liste der
offenen Chats konnte nur wachsen. Einen Reiter wieder loszuwerden war im
Programm gar nicht vorgesehen. Jetzt fragt die Liste nach jeder Handlung
neu nach, in jedem Tab, auch in den gerade nicht sichtbaren. Wenn das
Archivieren einmal nicht klappt, steht das ausserdem als Meldung da -
vorher sah ein Fehlschlag genauso aus wie ein Erfolg.

**Dasselbe gilt nach dem Qwirbeln.** Auch dort setzt das Programm den
Chat-Namen neu, und auch dort stand vorher weiter der alte im Reiter.
Was frisch geoeffnet und noch leer ist, verschwindet dabei nicht - ein
neuer Chat, in den man gerade erst hineinschreibt, bleibt stehen.

## v2.6.5 - Klecks ist jetzt ein Ordner, den man dazulegt

**Die eigene KI-Engine muss nicht mehr in jedes Paket.** Sie ist ein
Extra und kostet nichts - also gehoert sie auch nicht in einen Download,
den jemand herunterlaedt, der sie gar nicht will. Neu ist deshalb: den
Klecks-Ordner einfach neben oder in den Qwirbel-Ordner legen. Mehr ist
nicht zu tun. Qwirbel sucht ihn an den naheliegenden Stellen, findet ihn,
und ab dem naechsten Start ist er da. Kein Pfad eintragen, kein Haken
setzen, keine Einstellung suchen. Ein Ordner zaehlt uebrigens nur dann
als Engine, wenn auch wirklich etwas darin liegt - ein leerer Ordner mit
dem richtigen Namen wird nicht angenommen, denn sonst zeigt das Programm
auf eine Huelle und meldet spaeter Fehler, die niemand zuordnen kann.

**Und sie bekommt ihre eigene Python-Umgebung, so wie ComfyUI eine hat.**
Das Setup legt sie an, wenn ein Klecks-Ordner daliegt; im Programm gibt
es dafuer auch einen Knopf. Der Grund ist unspektakulaer und wichtig: auf
dem Entwicklungsrechner lief die Engine bisher mit der Umgebung von
ComfyUI mit. Auf jedem Rechner ohne ComfyUI waere sie damit gestorben,
und niemand haette gesehen warum. Wie wenig sie braucht, ist nachgezaehlt
worden - ausser der Standardbibliothek genau eine Bibliothek, auch fuer
den schnellen Grafikkarten-Weg. Deshalb dauert die Einrichtung rund
zwanzig Sekunden statt einer Kaffeepause. Am Ende wird nicht geglaubt,
dass es geklappt hat, sondern nachgeprueft.

**Klecks startet ab jetzt zusammen mit Qwirbel.** Das kostet keinen
Grafikspeicher - der Dienst ist nur ein kleiner Server, belegt wird die
Karte erst von einem geladenen Modell, und das laedt er von sich aus nie.
Liegt gar keine Engine herum, passiert schweigend nichts: wer sie nicht
hat, soll bei jedem Start nicht an etwas erinnert werden, das er nie
wollte.

**Der Werkzeugkasten redet nicht mehr so viel.** Wer viele MCP-Server
zugeschaltet hat, hatte bisher ein stilles Problem: von 138 Werkzeugen
standen 40 im Prompt, die uebrigen 98 kamen ueberhaupt nicht vor - nicht
gekuerzt, nicht erwaehnt, einfach unsichtbar. Fuer ein Modell besteht der
Unterschied zwischen "das gibt es nicht" und "danach muss ich fragen"
genau aus einem Satz. Der naheliegende Ausweg waere gewesen, alle Namen
aufzuzaehlen - das kostet aber Platz und schuettet mehr Heu auf die
Nadel. Jetzt steht dort stattdessen eine Zeile je Werkzeugkasten: was
drin ist, wie viel, und ein paar Beispiele. Rund ein Viertel der Kosten,
und der Blick geht von hundertdreissig Einzeldingen auf eine Handvoll
Kaesten. Dazu ein Satz, den man einem Modell offenbar sagen muss: nimm
kein Werkzeug, wenn die Aufgabe ohne geht.

## v2.6.4 - Ein Fehler, den die neuen Tests selbst nicht fanden

**In den beiden Versionen davor konnte der Agent keine Aufgabe mehr zu
Ende denken.** Das ist ein Fehler, der mit dem Umbau auf den waehlbaren
lokalen Motor hereingekommen ist, und er gehoert hier genannt statt
stillschweigend behoben. Der Agent gibt jedem seiner Denkschritte eine
Zeitgrenze mit - bei grossen Modellen bis zu 25 Minuten, weil ein
25-Milliarden-Modell auf einer normalen Karte langsam schreibt und ein
Abbruch nach zehn Minuten eine Luege waere. Die neue Zwischenschicht,
die entscheidet welcher lokale Motor rechnet, nahm dieses Feld nicht
entgegen. Der Aufruf brach ab, bevor irgendetwas gerechnet wurde.

**Warum es niemandem auffiel, obwohl fuenfzehn neue Pruefungen gruen
waren:** die Pruefungen sahen sich an, was die neue Schicht kann - nicht,
was ihr Aufrufer ihr schickt. Gefunden hat es am Ende eine ganz andere
Testdatei, die mit dem Umbau nichts zu tun hatte. Daraus sind drei neue
Pruefungen geworden, und sie stellen die Frage jetzt richtig herum: jedes
Feld, das der alte Weg entgegennimmt, muss der neue auch entgegennehmen,
und der echte Aufruf des Agenten wird Feld fuer Feld durchgespielt. Wer
etwas ersetzt, wird gegen das geprueft, was er ersetzt.

**Ausserdem bekommt die eigene Engine dieselbe Zeitgrenze.** Sie rechnete
bisher mit drei Minuten - fuer ein Gespraech richtig, fuer einen langen
Arbeitsauftrag zu wenig. Schlimmer als die Grenze selbst war die Meldung
danach: ein Abbruch sah aus wie "Dienst nicht erreichbar", also wie ein
ganz anderes Problem. Jetzt gilt dieselbe Zeit wie bei Ollama.

## v2.6.3 - Jede Antwort sagt, wer sie gerechnet hat

**Unter jeder Antwort steht jetzt, welcher Motor und welches Modell sie
wirklich gemacht haben.** Das klingt nach einer Kleinigkeit und ist
keine. Bisher konnte man das nur herausfinden, indem man das Modell
selbst fragte - und ein Modell weiss nicht, welches Modell es ist. Diese
Auskunft stammt aus seinen Trainingsdaten oder aus dem Programm-Text,
den Qwirbel ihm mitgibt, nicht aus Selbstbeobachtung. Ein kleines
Qwen-Modell antwortet mit voller Ueberzeugung, es sei ein grosses. Wer
so prueft, ob ein Modellwechsel funktioniert hat, prueft nichts.
Der neue Marker kommt aus der Abrechnung: dort steht ohnehin, wo die
Marken verbraucht wurden, und diese Angabe wird an der Stelle gesetzt,
an der wirklich gerechnet wird. Bei der eigenen Engine ist es sogar das
tatsaechlich geladene Modell und nicht das gewuenschte - das Etikett kann
also nicht neben der Wirklichkeit stehen. Steht die Zahl daneben nur auf
einer Schaetzung, sagt der Marker auch das.

**Die eigene Engine wird nicht mehr wie ein Cloud-Anbieter behandelt.**
Sie bekam kein "LOKAL - PRIVAT"-Schild, dafuer ein Eingabefeld fuer einen
API-Schluessel, den sie nie haben wird; sie zaehlte in der Liste der
Cloud-Anbieter mit und trug ein Schild, das automatisches Weiterreichen
versprach - obwohl sie genau das seit der letzten Version bewusst nicht
mehr tut. Der Grund war derselbe wie beim Leck, das die letzte Version
geschlossen hat: die Oberflaeche fragte an rund zwanzig Stellen nach
einem NAMEN, wo sie "ist das lokal?" meinte. Solange es nur einen
lokalen Motor gab, fiel das nicht auf. Jetzt gibt es dafuer eine
Antwort, und alle Stellen holen sie sich dort.

**Und die lokalen Motoren stehen oben.** Erst die eigene Engine, dann
Ollama, dann alles mit Schluessel. Wichtig dabei: die Reihenfolge wird
beim Laden durchgesetzt, nicht in einer Vorlage. Eine Vorlage haette bei
niemandem etwas geaendert, dessen Anbieter-Liste schon gespeichert ist -
und das ist nach dem ersten Start jeder. Innerhalb der uebrigen Anbieter
bleibt die eigene Reihenfolge unangetastet.

## v2.6.2 - Was lokal ist, bleibt lokal

**Wer Klecks als Motor gewaehlt hat, dessen Text konnte trotzdem bei
einem Cloud-Anbieter landen.** Das ist der wichtigste Punkt dieser
Version, und er war echt: waehlte man im Chat die eigene Engine und
schaltete Qwirbel bei einem Aussetzer automatisch weiter, stand Klecks
in seiner eigenen Ausweich-Kette gar nicht drin. Der naechste Schritt
war dann der erste bezahlte Anbieter in der Liste. Fuer Ollama gab es
diesen Schutz seit jeher - er war nur nie auf die zweite lokale Engine
uebertragen worden. Jetzt gilt er fuer beide: ein lokaler Start bleibt
lokal, auch wenn es hakt. Sechs neue Pruefungen halten das fest, und
eine davon nennt beim Fehlschlag ausdruecklich, welcher Anbieter den
Text bekommen haette.

**Der Token-Zaehler stand bei Klecks auf null.** Nicht ungefaehr,
sondern genau null: die Zaehlung schrieb ihre Zahlen unter Namen, die
niemand las, und ohne die Herkunftsangabe stieg die Buchung sofort
wieder aus. Wer ueber Ollama arbeitete, sah sein Tages-Budget wachsen;
wer ueber Klecks arbeitete, sah nichts - ohne eine einzige
Fehlermeldung. Klecks liefert jetzt die echten Zahlen mit, die der
Rechenmotor ohnehin schon zaehlt, und Qwirbel bucht sie. Fehlen sie
einmal, wird geschaetzt - und die Schaetzung ist als solche markiert,
statt sich als Messung auszugeben.

**Klecks durfte kein Modell laden, wo Ollama es durfte.** Dasselbe
Anliegen, dieselbe Grafikkarte, zwei verschiedene Antworten - je
nachdem, welchen Weg man genommen hatte. Der Grund war ein
verwechseltes Tor: Klecks fragte die Pruefung fuer Bildmodelle statt
die fuer Sprachmodelle. Gemessen sah das so aus, dass derselbe
Arbeitsschritt ueber Ollama in elf Sekunden durchlief und ueber Klecks
mit "Cloud-API-Key aktiv" abgewiesen wurde. Beide fragen jetzt dieselbe
Stelle.

**Und die Einstellung, welcher lokale Motor rechnet, tut endlich
etwas.** Sie stand seit einem Tag in der Konfiguration und wurde von
keiner einzigen Zeile gelesen - ein Schalter, den man umlegt und der
nichts aendert, ist schlimmer als gar keiner. Jetzt entscheidet er
wirklich, und deine ausdrueckliche Wahl im Chat schlaegt ihn: klickst
du Klecks an, bekommst du Klecks. Dazu gehoert eine Kleinigkeit mit
grosser Wirkung - Klecks legt sein Kontextfenster beim Start des
Modells fest, nicht pro Frage. Passt das geladene Fenster nicht zu dem,
was gerade gebraucht wird, sagt Qwirbel das mit beiden Zahlen und dem
Weg heraus, statt stillschweigend mit einem zu kleinen weiterzuarbeiten.

**Kleinigkeit am Rande:** eine leere Antwort gilt auch auf der
Qwirbel-Seite nicht mehr als Erfolg. Der Dienst weist sie schon selbst
ab - aber die Ehrlichkeit des Programms sollte nicht davon abhaengen,
dass sich am Dienst nie etwas aendert.

## v2.6.1 - Die Anzeige lebt

**Die Motor-Zeile unten links aktualisiert sich jetzt von selbst.**
Bisher fragte sie genau einmal beim Start - wer Klecks danach mit dem
Knopf startete, sah bis zum naechsten Neuladen weiter "OLLAMA". Jetzt
schaut sie alle acht Sekunden nach und springt von selbst um. Dasselbe
im Klecks-Tab: "Dienst nicht erreichbar" bleibt nicht mehr stehen,
wenn der Dienst laengst laeuft.

**Und der Klecks-Tab erfindet nichts mehr.** Antwortete der Dienst
nicht, zeigte die Modell-Liste sechs fest eingebaute Namen - die sahen
aus wie deine eigenen Modelle. Jetzt steht dort, dass nichts zu zeigen
ist, solange Klecks nicht laeuft. Die Kachel "VRAM belegt", die immer
leer war, ist einem Satz gewichen, der sagt, was die Zahl daneben
bedeutet: so viel darf ein Chat-Modell nehmen, der reservierte Platz
fuers Spielen ist schon abgezogen.

## v2.6.0 - Klecks rechnet mit

**Du kannst jetzt im Chat Klecks als Motor waehlen - deine eigene
Engine statt Ollama.** Im Modell-Menue steht „Klecks (eigene Engine)"
neben den anderen Anbietern; die Modelle sind dieselben, die schon auf
der Platte liegen, es wird nichts neu heruntergeladen. Auf einer
AMD-Karte laeuft der Vulkan-Weg gemessen rund 20 Prozent schneller beim
Schreiben. Ollama bleibt installiert und waehlbar - Klecks loest es ab,
wirft es aber nicht raus.

**Unten links steht ab jetzt der Motor, der wirklich rechnet.** Frueher
stand dort immer „OLLAMA RUNNING" - auch wenn gerade ein Cloud-Modell
oder gar nichts antwortete. Jetzt sagt die Zeile, wer da ist: laeuft
Klecks, steht dort Klecks (in seiner Farbe, und „rechnet", sobald ein
Modell auf der Karte liegt), sonst Ollama - und laeuft keiner von
beiden, sagt sie auch das, statt einen gruenen Punkt zu zeigen. Die
Knoepfe darunter bleiben, wo sie waren: Grafikkarte freiraeumen,
Einstellungen, Oberflaeche neu laden.

**Und Klecks kann jetzt mit Qwirbels Wissen arbeiten.** In Klecks gibt
es eine neue Gruppe von Bausteinen fuer Sprachmodelle - darunter einen,
der dein Kernwissen holt und dem Modell als Rahmen mitgibt. Weil das
gesammelte Wissen viel groesser ist als das Gedaechtnis eines Modells,
wird ausgewaehlt statt alles hineingeschoben: mit Stichworten die
passenden Fakten, ohne Stichworte reihum aus jedem Bereich. Was nicht
mehr hineinpasste, wird dazugesagt - nicht verschwiegen.

## v2.5.0 - Klecks zieht ein

**Klecks hat jetzt ein eigenes Tab in Qwirbel - neben ComfyUI, nicht
statt ComfyUI.** Klecks ist das zweite Programm: eine Node-Oberflaeche,
die Bilder auf Vulkan rechnet und seit dieser Version auch Chat-Modelle
faehrt. Im Tab siehst du seine Oberflaeche direkt im Fenster, kannst auf
"Steuerung" umschalten und dort sehen, welches Modell gerade auf der
Karte liegt, wieviel Speicher frei ist, und Modelle mit einem Klick
laden oder wieder rauswerfen. ComfyUI bleibt vollstaendig, wo es war -
du entscheidest, womit du arbeitest.

**Laeuft Klecks nicht, startet Qwirbel es fuer dich.** Frueher haettest
du in einen anderen Ordner gehen und doppelklicken muessen. Jetzt steht
im Tab, dass der Dienst aus ist, und daneben ein Knopf. Und keine
Sorge um die Grafikkarte: der Dienst selbst belegt nichts - Speicher
kostet erst ein Modell, das du wirklich laedst.

**Chat-Modelle laufen wahlweise ueber Klecks (Vulkan) statt ueber
Ollama.** Der Vorteil ist gemessen, nicht behauptet: auf einer
AMD-Karte erzeugt der Vulkan-Weg rund 20 Prozent mehr Text je Sekunde.
Die Modelle bleiben, wo sie liegen - es wird nichts neu
heruntergeladen. Umgestellt wird erst, wenn der neue Weg bei dir
nachweislich gleich gut laeuft; bis dahin bleibt Ollama der Standard.

**Wenn nichts herauskommt, sagt Qwirbel warum.** Manche Modelle denken
erst nach, bevor sie antworten. War das Antwort-Budget zu klein, ist
das Nachdenken fertig und die Antwort leer - frueher waere dir einfach
eine leere Blase erschienen. Jetzt steht da, was passiert ist und was
du drehen kannst. Dasselbe beim Rauswerfen eines Modells: gemeldet wird,
was wirklich passiert ist, nicht was passieren sollte.

**Und der Platz zum Spielen bleibt frei.** Qwirbel und Klecks teilen
sich eine Grafikkarte mit deinen Spielen. Der reservierte Rest galt
bisher nur beim Bildermachen - jetzt auch fuer Chat-Modelle. Ein
grosses Modell nimmt dir die Karte also nicht mehr komplett weg.

## v2.4.0 – Der Chat bleibt beim Reden

**Kleine Modelle stolpern im Chat nicht mehr ueber Werkzeuge, die es dort
gar nicht gibt.** Bisher bekam das Modell im Chat die komplette
Werkzeug-Doku gezeigt – auch Bauen, Ordner anlegen, Programme starten. Ein
kleines Modell probierte dann genau das und lief in die Sperre: du fragtest
nach einer Website und bekamst drei geblockte Fehlversuche statt einer
Antwort. Jetzt sieht das Modell im Chat nur noch, was der Chat wirklich
kann – nachschauen, lesen, Websuche, Seiten durchklicken, Bilder ansehen
und erzeugen. Im echten Test war der Unterschied sofort da: vorher sechs
Zuege mit drei geblockten Versuchen und einer Rueckfrage, jetzt eine
direkte Antwort mit Quelle.

**Deine eigene URL braucht keine Rueckfrage mehr.** Schreibst DU eine
Adresse in den Chat („schau dir beispiel.de an"), ist das die Erlaubnis –
Qwirbel holt die Seite, ohne erst zu fragen, ob die Domain auf der
Freigabe-Liste steht. Die Schutzmauern bleiben: Adressen, die sich das
Modell selbst ausdenkt, fremde IP-Adressen und kaputte Links laufen weiter
durch die normale Pruefung.

**Modelle ohne Werkzeug-Training reden einfach – und du siehst es vorher.**
Manche Modelle (z.B. gemma3) koennen von Haus aus keine Werkzeuge bedienen.
Die tragen jetzt im Modell-Menue die Markierung „redet nur". Waehlst du so
ein Modell und fragst nach einer Website, holt Qwirbel die Seite selbst und
legt sie dem Modell vor – du bekommst trotzdem eine Antwort. Und wo es
wirklich Werkzeuge braeuchte, sagt Qwirbel dir ehrlich, dass dieses Modell
nur reden kann, statt minutenlang herumzuprobieren.

**„Hey Qwirbel" antwortet jetzt hoerbar.** Nach dem Weckwort spielt ein
kurzer Ton, sobald die Aufnahme wirklich laeuft – und ein zweiter, wenn sie
zu Ende ist. Du musst nicht mehr auf den Bildschirm schauen, um zu wissen,
ob dein Diktat ankommt. Funktioniert auf Windows, macOS und Linux mit
Bordmitteln, ganz ohne Zusatz-Software.

**Neu: die Chat-Bibliothek – tausende Modelle, jede Quantisierung, ein
Klick.** Im Models-Bereich gibt es jetzt den Tab „Chat-Bibliothek": ueber
800 GGUF-Chat-Modelle der grossen Quantisierer (unsloth, bartowski), sortiert
nach Beliebtheit, mit Suche. Jedes Modell laesst sich aufklappen und zeigt
seine Quantisierungen mit ECHTER Groesse in GB und einem Haken, ob sie auf
deine Grafikkarte passt – ein Klick laedt genau diese Variante. Der Knopf
„Von Hugging Face aktualisieren" holt jederzeit die frische Liste (nur die
Liste – heruntergeladen wird erst, wenn DU auf Laden drueckst).

**Der Model-Store sagt dir jetzt, was ein Modell WIRKLICH kann.** Jedes
Modell traegt neben Groesse und VRAM-Haken zwei neue, ehrliche Marken:
WERKZEUGE (kann nachschauen – Websuche, Dateien, Seiten bedienen) oder
„redet nur" (reines Reden, Bilder verstehen). Damit siehst du VOR dem
Laden, ob ein Modell in den Chat-Alltag passt oder nur zum Plaudern taugt –
bisher sah ein reines Rede-Modell im Store genauso aus wie ein
Arbeits-Modell, und die Enttaeuschung kam erst hinterher.

## v2.3.0 – Ein Setup, das dich fragt

**Doppelklick, und ein Fenster fuehrt dich durch die Einrichtung.** Bisher
oeffnete das Setup ein schwarzes Konsolenfenster mit drei Knoepfen, und ab da
entschied es selbst. Jetzt kommt ein richtiger Assistent – sechs Schritte, in
denen DU bestimmst, und am Ende eine Uebersicht, auf der alles nochmal steht.
Bis du dort auf „Installieren“ drueckst, wird nichts angefasst. Wer das nicht
will, drueckt auf der ersten Seite „Schnell installieren“ und ist mit den
Vorgaben durch.

**Du waehlst, wohin – auch auf eine andere Festplatte.** Vorgabe bleibt der
Programme-Ordner deines Nutzers (derselbe Ort wie Ollama, ohne Admin-Abfrage).
Genauso geht `C:\Program Files` oder ein eigener Ordner auf einer anderen
Platte. Der Assistent zeigt je Laufwerk den echten freien Platz, sagt dir
vorher, wieviel gebraucht wird, und warnt, wenn Windows nach Admin-Rechten
fragen wird oder dort schon eine Installation steht.

**Wo die KI-Modelle liegen, entscheidest du beim Einrichten.** Modelle sind
gross – ein 7B-Modell rund 5 GB, ein 70B-Modell rund 40. Statt sie erst auf
die Systemplatte zu legen und spaeter umzuziehen, waehlst du den Ordner
sofort. Qwirbel setzt dafuer `OLLAMA_MODELS` fuer deinen Benutzer, ohne
Admin-Rechte.

**Deine Daten kommen mit – und du siehst vorher, welche.** Hast du Qwirbel
schon benutzt, sucht der Assistent den alten Ordner: Desktop, Dokumente,
Downloads, `D:\Qwirbel`, eine aeltere Installation. Findet er mehrere,
kannst du waehlen; liegt deiner woanders, zeigst du per „Durchsuchen …“
hin. Er sagt dir dann ehrlich, ob dort ueberhaupt ein Qwirbel steckt und
welche Version. Uebernommen wird nach Gruppen mit Haken – Chats, Wissen,
Einstellungen, Workflows, Sprach-Modell, Arbeitsordner, Profile,
Automatik-Laeufe – jede mit gemessener Groesse und Dateizahl daneben. Der
Stand am Ziel wird vorher automatisch gesichert.

**Drei Sachen, die beim Uebernehmen bisher liegenblieben.** Das Sprach-Modell
fuer „Hey Qwirbel“ (`training/`) wurde nie mitgenommen – nach einem Umzug
reagierte das Weckwort schlicht nicht mehr, ohne dass irgendwo etwas stand.
Ebenso fehlten der Modell-Katalog der Generation und die Protokolle der
Automatik-Agenten. Alles drei kommt jetzt mit. Umgekehrt bleibt der
Browser-Cache des Fensters jetzt draussen: der wurde bisher mitkopiert und
brachte allein 305 MB Wegwerf-Daten mit, die beim ersten Start ohnehin neu
entstehen.

**Die Lizenz wird beim Einrichten geklaert, nicht erst beim ersten Start.**
Der Assistent findet eine vorhandene Aktivierung im gewaehlten Ordner und
uebernimmt sie, oder du gibst den Schluessel ein und er wird am Ende
freigeschaltet. Beides laesst sich ueberspringen. Klappt die Freischaltung
nicht, ist die Installation trotzdem fertig – und es steht da, statt still
zu scheitern.

**Auch der Server bekommt eine EXE.** Bisher gab es die nur fuer die
Einzelplatz-Fassung; Firmenkunden bekamen ein ZIP und eine Batchdatei. Jetzt
gibt es `Qwirbel-Server-Setup` genauso.

**Die Colibri-Engine stirbt jetzt mit Qwirbel.** Vorher lief `coli serve`
nach dem Schliessen einfach weiter und hielt Port 8000 besetzt – aufgeraeumt
wurde erst beim naechsten Start. Ein Herunterfahr-Haken allein reicht dafuer
nicht, denn bei einem harten Beenden laeuft der nicht: die Engine haengt
jetzt in einem Windows-Job-Objekt, das der Kernel mit abraeumt, egal wie
Qwirbel endet.

**Und die Colibri-Karte zeigt nicht mehr gruen, wenn nichts geht.** Colibris
`/health` antwortet weiter mit „ok“, auch wenn der Dispatcher der Engine
gestoppt ist und jede Anfrage mit Fehler 500 zurueckkommt. Qwirbel hat dem
geglaubt und „laeuft“ angezeigt, waehrend das Modell nie antwortete. Jetzt
wird der Zustand „gestoert“ gemeldet, mit der Zeile aus dem Motorprotokoll
im Klartext dazu.

## v2.2.0 – Bewegte Hintergruende und Glas bis ganz links

**Dein Wallpaper laeuft jetzt IN Qwirbel.** Als Programm-Hintergrund geht
neben einem Bild jetzt auch ein Video (MP4/WebM) – hochladen, fertig. Es
laeuft in Schleife, ohne Ton, hinter der ganzen Oberflaeche, und der
Blur-Regler wirkt darauf genauso wie auf ein Bild. Das Video wird einmal
gespeichert und gilt fuers ganze Programm, auf allen Geraeten.

**Die Wallpaper-Bibliothek deines PCs, ein Klick entfernt.** Qwirbel schaut
auf Wunsch selbst nach, welche Kurzvideos deine Wallpaper-Programme schon auf
der Platte haben: Wallpaper Engine (Steam, alle Bibliotheken), ScreenPlay und
Lively. Die Funde erscheinen als Kacheln mit Vorschaubild – ein Klick, und
das Video ist dein Hintergrund. Es wird dabei KOPIERT: loeschst du das
Wallpaper-Programm, bleibt dein Hintergrund heil. Und die Anzeige ist
ehrlich: Wallpaper vom Typ Scene oder Web sind keine Videos – die kann nur
Wallpaper Engine selbst abspielen. Statt still weniger anzuzeigen, sagt dir
Qwirbel jetzt, wie viele deiner Wallpaper aus genau dem Grund nicht gehen.

**Die linke Tab-Leiste wird zu Glas.** Mit eigenem Hintergrund (Bild oder
Video) ist die Leiste jetzt durchsichtig und nimmt denselben Weichzeichner an
wie die Kopfzeile oben – dein Hintergrund laeuft in einem Stueck durchs ganze
Fenster, statt links an einer Blech-Saeule zu enden. Ohne eigenen Hintergrund
bleibt alles wie gewohnt.

**Der Chat schaut sofort ins Netz, statt in deinen Ordnern zu suchen.**
Sagst du „schau auf die Website …" oder nennst einen Link, holt Qwirbel die
Seite jetzt SOFORT – noch bevor das Modell seinen ersten Zug macht. Vorher
konnte gerade ein kleines Modell auf die Idee kommen, erst einmal Dateien
und Ordner zu durchsuchen, obwohl die Antwort im Internet steht. Auch das
Planen entfaellt bei einer reinen Web-Frage: Seite holen, antworten. Datei-
und Ordner-Werkzeuge sind fuer solche Fragen ausdruecklich gesperrt – auch
dann, wenn du vorher Bilder oder Dateien in den Chat gelegt hast.

**Jeder Settings-Tab hat unten eine Frage: Welche Einstellung brauchst du?**
Schreib hinein, was du willst – „mach mir ein dunkelrotes Theme“, „Video-
Hintergrund mit wenig Blur“, „fuege das Modell glm-4.6 hinzu“ – und Qwirbel
stellt es ein. Beim Modell schaut er dafuer selbst im Netz nach, wie gross
dessen Kontextfenster wirklich ist, statt zu raten. Was er dabei aendern
darf, ist je Tab fest umrissen: alles andere lehnt das Programm ab, auch
wenn das Modell es vorschlaegt. In Tabs, in denen nichts automatisch
verstellt werden soll (Verbindung, Shortcuts, KI & Filter, Stimme, Menue),
antwortet die Box nur – sie sagt dir, wo die Einstellung sitzt. E-Mail und
Verlauf haben bewusst keine Box.

**Jedes MCP-Werkzeug gehoert jetzt selbstverstaendlich dazu.** Was du an
MCP-Servern zuschaltest, benutzt der Agent aktiv, statt daneben schlecht zu
improvisieren – und ein fehlerfreier MCP-Lauf zaehlt als echter Beleg.
Scheitert ein Aufruf, versucht er es einmal neu (der Verbinder repariert
bekannte Defekte dabei selbst) und nennt dir sonst die Fehlermeldung im
Wortlaut. Fehlt ihm fuer einen Schritt ein Werkzeug, das es als MCP-Server
gaebe, sagt er dir KONKRET, welchen du zuschalten sollst.

**Roblox & Co: der Agent nutzt jetzt die MCP-Bruecke.** Roblox, Unity,
Blender und Godot laufen auf einem normalen Rechner nicht – bisher konnte der
Agent dort nur bauen und ehrlich sagen: nicht getestet. Jetzt gilt: Sind
passende MCP-Werkzeuge verbunden (z.B. ein Roblox-Studio-MCP-Server), MUSS er
sie benutzen – Code einfuegen, wirklich ausfuehren, die Ausgabe lesen – und
erst ein fehlerfreier Lauf darueber zaehlt als Test. Sind keine verbunden,
empfiehlt er dir im Schlussbericht konkret, einen passenden MCP-Server ueber
den MCP-Chip zuzuschalten. Ist einer zugeschaltet, der nicht verbindet, nennt
er den Grund, statt Tests zu behaupten. Und ein fremder MCP-Lauf (etwa eine
Datenbank-Abfrage) kauft weiterhin kein „getestet" frei.

**Der Chat merkt sich jetzt, welche Dateien er schon kennt.** Bisher wusste
Qwirbel das nur INNERHALB eines Auftrags – im selben Chat den naechsten
gegeben, und er las dieselben Dateien wieder von vorn. Jetzt fuehrt jeder
Chat einen Merkzettel: welche Datei, wie gross, was am Anfang steht. Der
steht in jedem Arbeitsschritt vor ihm, mit der klaren Ansage: nicht blind
nochmal alles oeffnen. Und er ist ehrlich – vor jeder Anzeige wird gegen die
Platte geprueft: hat sich eine Datei seither geaendert, steht "neu lesen"
dabei; ist sie weg, steht das auch da. Beim Qwirbeln wird der Merkzettel
zusammen mit dem Chat ausgewertet und geleert.

**Die Kopf-Platz-Anzeige zeigt endlich, wohin die Tokens wirklich gehen.**
"Dateien" stand dauerhaft auf 0 %, obwohl Qwirbel den halben Tag Dateien
gelesen hat – die Lese-Ergebnisse liefen alle unter "Tools". Jetzt zaehlen
Datei-Werkzeuge in ihre eigene Spalte. Auch dann, wenn das Lesen ueber einen
MCP-Server laeuft: ein `read_multiple_files` ueber MCP ist Datei-Platz, kein
MCP-Kleinkram. Genau dieses Lesen lief bisher auch am Merkzettel vorbei –
daher las er ueber MCP immer wieder dieselben Dateien.

**Zwei Dinge baut Qwirbel jetzt grundsaetzlich nicht mehr.** Schadsoftware –
Ransomware, Keylogger, Trojaner, Spyware, etwas das sich heimlich
installiert oder den Virenschutz umgeht – ist fest gesperrt, auch wenn in
der Anfrage gar kein Opfer steht. Ebenso Lizenz- und Kopierschutz zu
umgehen: keine Cracks, keine Keygens, keine Raubkopien. Beides laesst sich
nicht ueber die Filterstufe abschalten, es gehoert zum Grundgesetz.

**Und genauso wichtig: er blockt deine Arbeit deswegen nicht.** „Mach meine
Website sicher“, „entferne den Trojaner aus meinem Programm“, „wie schuetze
ich mich vor Ransomware“, „wie werde ich das wieder los“, „was ist
eigentlich ein Keylogger“, „ich habe meinen gekauften Schluessel verloren“
– das alles ist normale Arbeit und laeuft durch. Genau diese Trennung wird
ab jetzt bei jeder Aenderung automatisch geprueft: eine eigene Testreihe
haelt beide Richtungen fest – Missbrauch blockt, Arbeit laeuft. Beim Bau
hat sie zwei Faelle gefunden, in denen der neue Schutz ehrliche Auftraege
verschluckt haette.

**Kleinkram:** Das neue Werkzeug `agenten_stopp` aus v2.1.0 hatte zwei der
vier Pflicht-Eintraege nicht (Wirkungs-Klasse und Anzeige-Label) – in
unbeaufsichtigten Laeufen waere der geordnete Schwarm-Stopp dadurch still
geblockt gewesen; jetzt vollstaendig. Upload-Grenzen fuer den Hintergrund:
Bilder 12 MB, Videos 512 MB – Videos werden gestueckelt auf die Platte
geschrieben statt komplett in den Arbeitsspeicher geladen.

## v2.1.0 – Er vergisst nicht mehr mitten in der Arbeit

**Das grosse Modell durfte die ganze Zeit nur einen Bruchteil seines
Gedaechtnisses benutzen.** Wer eine Aufgabe mit GLM laufen liess, bekam ein
Verlaufs-Budget von 19.464 Zeichen – das ist das Fenster des KLEINEN lokalen
Modells. GLM kann 1.159.488. Der Grund: bei einem bestaetigten Plan wurde der
Modellname nicht mit weitergereicht, der Aufruf nahm dann still das erste
Modell des Anbieters, und die Budget-Rechnung fiel mangels Namen auf das
lokale Fenster zurueck. Beides fragt jetzt dieselbe Stelle. Das ist der Grund,
warum er in langen Auftraegen dieselben Dateien immer wieder gelesen hat: was
er zwei Zuege vorher gelesen hatte, war schon wieder aus seinem Kopf.

**Wird der Platz wirklich knapp, wird zuerst gesichert – dann erst gekuerzt.**
Bei 90 Prozent legt er den vollstaendigen Chat nach `chats/exports/` und
schreibt den Pfad in den Verlauf. Vorher schnitt der normale Chat hart bei
6000 Zeichen ab, ohne ein Wort zu sagen – egal ob das Modell 16k oder 976k
Token traegt. Jetzt richtet sich das Fenster nach dem Modell, das wirklich
laeuft (Obergrenze einstellbar unter `chat.kontext_max_zeichen`).

**Angeheftete Zeilen ueberleben jetzt auch das Vergessen.** Ein Eintrag mit
`[PIN]` blieb zwar in der Kompression erhalten – wurde er aber aelter als die
letzten zwoelf eigenen Nachrichten, fiel er trotzdem ersatzlos aus der
Kurzfassung. Angeheftetes wird jetzt aus dem gesamten Verlauf geholt, egal wie
alt.

**Im Chat-Tab sind wieder alle Modelle waehlbar.** Die 30B-Schranke gilt dort,
wo sie gemeint war: in Work und Code. Im Chat und im Mind-Tab darf jedes
Modell nachschauen und planen – die Werkzeuge bleiben dabei unveraendert eng
(lesen, nachschlagen, Webseiten ansehen; nichts Schreibendes). Die Auswahl
oben rechts richtete sich vorher nach dem Tab, der zuletzt gerechnet hatte,
nicht nach dem, in dem man steht.

**Der QWIRBELN-Knopf nimmt das Modell aus der Leiste.** Steht dort GLM, fasst
GLM zusammen. Vorher lief immer das lokale Standardmodell, egal was gewaehlt
war – das Backend konnte es laengst, es bekam die Auswahl nur nie gesagt.

**Einen Agenten-Schwarm kann er jetzt selbst geordnet beenden.** Neues
Werkzeug `agenten_stopp`: es sagt allen Helfern Bescheid, laesst sie ihren
Zug zu Ende bringen und bricht nur ab, wer nach der Frist noch haengt. Vorher
gab es dafuer nur den Knopf in der Oberflaeche oder einen harten Abbruch
mitten in der Arbeit.

**Qwirbel startet nur noch einmal.** Ein zweiter Start scheiterte bisher zwar
am Port, lief danach aber weiter und machte ein zweites Fenster samt zweitem
Symbol auf. Jetzt meldet er sich sauber ab und weist auf das laufende Fenster
hin. Abgestuerzte Reste blockieren nichts.

**In erzeugten Dateien steht jetzt, WELCHES Modell sie geschrieben hat.** Die
Kennzeichnung nach Art. 50 EU-KI-VO nennt zusaetzlich Modell und Herkunft –
"mit glm-5.3 ueber zai (Cloud-API)" oder "mit qwen3 lokal (Ollama)" – auch in
den Metadaten von Bildern und Videos.

**Kleinkram:** Unbekannte Cloud-Modelle bekommen ein eigenes, konservatives
Fenster statt des lokalen, dazu eine Zeile im Protokoll; neue Modelle lassen
sich ohne Code-Aenderung unter `modell_kontext` in der Konfiguration
eintragen. Ein kaputter Eintrag beim Kontext-Fenster fuehrt nicht mehr zu
einem Budget von null.

## v2.0.0 – Diktieren wie Tippen, und alles ist einstellbar

**Der Text kommt jetzt beim Sprechen, nicht danach.** Der Mikro-Knopf im Chat
arbeitet in zwei Stufen: ein schnelles Modell schreibt grau mit, während man
noch redet, ein genaues bestätigt kurz darauf – und Bestätigtes steht sofort
als normaler Text im Eingabefeld. Gemessen auf einem Ryzen 7: die erste Anzeige
kommt nach ~1,3 Sekunden statt nach ~3,6, und sie aktualisiert sich alle 0,6
Sekunden statt in unregelmäßigen Abständen von bis zu 3,7 Sekunden. Zwischen
zwei Sätzen steht die Anzeige nicht mehr still.

**Die Eingabezeile wächst nur noch so weit, wie wirklich Text da ist.** Vorher
sammelte sich das ganze Diktat als grauer Block in der Zeile, sie wuchs immer
weiter und ging nie wieder zurück. Jetzt wächst sie wie beim Tippen mit,
schrumpft wieder und hört nach etwa sieben Zeilen auf – dann wird gescrollt.

**Der Empfindlichkeits-Regler funktioniert über den ganzen Weg.** Ab Stufe 2,2
lag die Sprach-Schwelle rechnerisch unter dem Rauschen des eigenen Mikrofons:
das Mikro hörte sich selbst als Sprache, kein Satz wurde je abgeschlossen, und
in der Zeile stand ein Textblock, der bis zum Stopp immer wieder neu
geschrieben wurde. Die Schwelle liegt jetzt in jeder Stellung über dem
Grundrauschen und wird während der Aufnahme laufend nachgeführt – dreht die
Lüftung auf, rutscht sie mit.

**Wer ohne Pause durchredet, verliert nichts mehr.** Nach einer einstellbaren
Länge wird beim nächsten Atemholen geschnitten und das Stück bestätigt, statt
den ganzen Vortrag als eine wachsende, immer langsamere Vorschau zu führen.
Umgekehrt erzeugt reines Rauschen jetzt gar keinen Text mehr: die typischen
Untertitel-Sätze, die Spracherkennungen bei Stille erfinden, werden erkannt und
verworfen.

**Neu in den Einstellungen (Stimme → Mikrofon-Diktat):** Vorschau-Modell
(oder aus), Vorschau-Takt, wann eine Sprechpause einen Satz beendet und wie
lang ein Stück am Stück höchstens wird. Dazu steht jetzt dabei, welche Regler
für das Live-Diktat im Chat gelten und welche für die Einzel-Aufnahme
(Test-Diktat und Hotword) – diese Trennung war vorher nicht zu erkennen.

**Wenn du über eine API arbeitest, bleibt deine Grafikkarte in Ruhe.** Das war
der hartnäckigste Fehler dieser Reihe: Qwirbel beantwortete deine Frage über
Claude, GLM oder Gemini – und holte sich nebenbei trotzdem ein lokales Modell
in den Speicher. Für den Chat-Namen. Für die Einsortierung deiner Nachricht.
Für das Nachlernen danach. Auf einer 16-GB-Karte mit einem großen Modell
bedeutet das: der Rest wandert in den Arbeitsspeicher, und der Rechner kriecht
minutenlang – bei manchen stundenlang, ohne dass sichtbar etwas passiert.
Nachgemessen war es am Ende eindeutig: 15,7 GB belegt, vier Minuten nachdem
„Speicher freigeben" gedrückt worden war, während die letzte Antwort über eine
Cloud-API lief. Es gibt jetzt genau **eine Stelle**, durch die jeder Modell-Start
muss, und dort gilt: hast du oben rechts einen Anbieter gewählt, läuft alles
dort – auch Nebensachen wie Chat-Namen oder Zusammenfassungen. Lokal wird dafür
nichts geladen.

**Beim Programmstart geht kein Modell in die Grafikkarte.** Vorher konnte schon
das bloße Hochfahren etwas nachladen. Jetzt lädt ein Modell erst, wenn du
wirklich etwas machst – ein Prompt, ein Auftrag, ein Knopf. Und: was Qwirbel
**nebenbei** denkt (Namen vergeben, einsortieren, nachlernen, Scans
zusammenfassen), lädt **nie** ein Modell nach. Es darf nur mitbenutzen, was
ohnehin schon im Speicher liegt. Wird eine solche Nebensache deshalb
übersprungen, steht der Grund im Protokoll statt nirgendwo.

**Neu einstellbar: womit soll nebenbei gedacht werden?** Unter dem Zahnrad
(siehe unten) wählst du für Qwirbeln, Nachlernen, Chat-Namen und Scans zwischen
**über API** (nichts belegt die Grafikkarte), **lokal** (wie früher, mit dem
Modell, das ohnehin geladen ist) und **aus** (Qwirbel denkt gar nicht nebenbei).
Anbieter und Modell dafür sind frei wählbar – gerade bei langen Chats mit
30.000 Zeichen und mehr macht es einen Unterschied, ob das ein großes
Cloud-Modell zusammenfasst oder der kleine Rechner nebenan.

**Der Chat schickt dich nicht mehr bei jeder Kleinigkeit in den Work-Tab.**
„Schau auf der Seite nach", „guck dir die drei Bilder an", „formulier mir eine
Antwort-Mail", „mach mir ein Bild davon" – das sind Gespräche, keine Bauprojekte.
Der Chat kann dafür jetzt **44 der 90 Werkzeuge** selbst benutzen (vorher 24):
Seiten öffnen, darauf klicken und tippen, Bilder und Videos ansehen, im Netz
recherchieren, Bilder und Videos erzeugen, deine Post ansehen, Termine
eintragen, in die Zwischenablage schauen. Er darf bis zu zwölf Schritte am Stück
machen statt sechs. In den Work-Tab geht es nur noch, wenn wirklich etwas
Dauerhaftes entsteht: ein Programm, eine Datei, ein geschnittenes oder
hochgeladenes Video, eine Installation. Schreiben, Shell-Befehle, Kompilieren
und der Agenten-Schwarm bleiben dem Work- und Code-Tab vorbehalten – im Chat
kann dir also weiterhin nichts kaputtgehen.

**Oben rechts in Work und Code sitzt jetzt ein Zahnrad.** Nicht in der
Eingabezeile, sondern dort, wo die Reiter sind – und es gilt für genau diesen
Tab. Darin: Prompt-Zwischenspeicher (für diesen Tab und global), ob ein Chat bei
seinem Anbieter bleibt, ab welcher Größe ein lokales Modell diesen Tab überhaupt
fahren darf, mit welchem Kontextfenster lokal geladen wird, und die eben
beschriebene Wahl fürs Qwirbeln. Jeder Wert dort **ist** die Einstellung – es
gibt keine zweite Stelle mehr, an der etwas anderes stehen könnte. Zwei Schalter
haben dabei vorher nur so getan als ob: sie wurden gespeichert und nie gelesen.
Das ist behoben, und die Anzeige daneben sagt dir, wie viele deiner Modelle
diesen Tab gerade fahren dürfen.

**Work und Code nehmen nur Modelle, die die Arbeit tragen.** Zu kleine Modelle
verschwinden nicht aus der Liste, sie werden **ausgegraut und sagen im
Tooltip, warum** – zu wenig Parameter oder ein Kontextfenster, das für den
bisherigen Verlauf nicht reicht. Dabei ist ein echter Zählfehler aufgefallen:
ein 8-Milliarden-Modell wurde als 14,8 Milliarden ausgewiesen und wäre so an
der Grenze vorbeigekommen. Und die angezeigte Fenstergröße ist jetzt die, mit
der Qwirbel wirklich lädt – nicht die, die das Modell theoretisch könnte.

**Qwirbeln geht jetzt der Reihe nach.** Drückst du in einem zweiten Chat
QWIRBELN, während der erste noch läuft, stellt er sich an: am Knopf steht die
Zahl, im Fortschritt steht dein Platz, und die Läufe gehen nacheinander durch.
Vorher rechneten zwei große Zusammenfassungen gleichzeitig auf derselben
Grafikkarte.

**Die Websuche funktioniert wieder.** Sie hing an einer einzigen Quelle, und die
antwortet seit einiger Zeit nur noch mit einer Bot-Sperre. Schlimmer als der
Ausfall war, dass es still passierte: Qwirbel bekam „nichts gefunden" statt
„Suche kaputt", formulierte um und suchte weiter ins Leere. Jetzt ist es eine
Kette – Brave, dann Marginalia, dann Wikipedia – und wenn wirklich nichts geht,
sagt er das. Für die vollwertige Suche kannst du unter **Einstellungen →
Verbindung** einen kostenlosen Brave-Schlüssel eintragen (2000 Anfragen im
Monat); ohne Schlüssel läuft sie über die freien Quellen weiter.

**Was Qwirbel schreibt, sagt jetzt, dass es von Qwirbel ist.** Bilder, Video und
Ton trugen die Kennzeichnung schon; neu sind Texte und Code. In eine Datei, die
Qwirbel anlegt, kommt eine Herkunftszeile in der Kommentar-Schreibweise der
jeweiligen Sprache – ohne die Datei kaputtzumachen (Startzeilen, Dokumenttypen
und Formate ohne Kommentare bleiben unangetastet). Fremde Dateien, die er nur
bearbeitet, bekommen keinen Stempel: er behauptet keine Urheberschaft, die ihm
nicht gehört.

**Wiederholte Anfragen an eine API werden billiger, und Anbieterwechsel werden
angesagt.** Der lange, immer gleiche Teil einer Anfrage wird beim Anbieter
zwischengespeichert. Gemessen mit einem echten Schlüssel und einem echten
Arbeits-Prompt: 5760 von 5800 Zeichen-Einheiten kamen aus dem Zwischenspeicher,
der einzelne Schritt war **49,6 % günstiger**. Dazu merkt sich jeder Chat seinen
Anbieter. Wechselst du mitten im Gespräch, ist der Zwischenspeicher weg und es
kostet wieder voll – deshalb sagt Qwirbel den Wechsel jetzt an, statt ihn still
zu machen. Verhindert wird er nie.

**Diktat: Sprache wählbar, und das Weckwort startet es mit.** Deutsch, English
oder automatisch – die Einstellung ist kein Feinschliff: mit der falschen
Einstellung **übersetzt** die Spracherkennung deinen deutschen Satz ins
Englische, statt ihn mitzuschreiben. Und wer das Weckwort benutzt, bekommt jetzt
dasselbe Live-Diktat wie über den Knopf: man liest beim Sprechen mit, statt ins
Blaue zu reden. Knopf und Weckwort geben sich das Mikrofon sauber weiter.

**Qwirbel trägt sich nirgends in den Autostart ein.** Auf keinem Weg, auf keiner
Stufe, auch nicht für ein anderes Programm – weder über die Registry noch über
den Autostart-Ordner, noch über Aufgabenplanung, systemd oder cron. Grund ist
nicht Bequemlichkeit, sondern dass genau dieses Muster jede
Verhaltenserkennung auslöst; einmal hat ein Virenscanner Qwirbel deswegen
mitten in der Arbeit abgeschossen. **Lesen und Abschalten bleiben erlaubt** –
das Privacy-Center räumt weiter auf, nur das Eintragen ist zu. Willst du
Autostart, sagt Qwirbel dir den Weg und öffnet dir den Ordner.

**Mac: die Installations-Anleitung stimmt jetzt für aktuelles macOS.** Ab
macOS 15 (Sequoia) und 26 (Tahoe) bietet das Sperr-Fenster bei
heruntergeladenen Dateien nur noch „Schließen" oder „In den Papierkorb" – der
alte Trick Rechtsklick → Öffnen funktioniert dort **nicht mehr**, und genau
darauf lief unsere Anleitung hinaus. Ein Kunde auf einem Mac mini M4 hing
deshalb fest und musste sich selbst durch die Datei-Attribute arbeiten. Jetzt
steht ganz oben der Weg, der immer geht: eine Zeile ins Terminal kopieren, den
Ordner hineinziehen, fertig. Dazu der Sequoia/Tahoe-Weg über
„Datenschutz & Sicherheit → Trotzdem öffnen", der alte Weg für ältere Systeme,
und die Ansage, dass Qwirbel sich selbst nach `/Applications` zieht – du darfst
den entpackten Ordner in „Downloads" liegen lassen.

**Neu erklärt: KI-Modelle auf eine externe Festplatte.** Das Große sind nicht
Qwirbel, sondern die Modelle (5–20 GB pro Stück), und die gehören Ollama. In
der Mac-Anleitung steht jetzt Schritt für Schritt, wie man sie umzieht
(`OLLAMA_MODELS`), wie es einen Neustart übersteht – und was passiert, wenn die
Platte mal nicht angesteckt ist: Ollama meldet dann eine leere Liste und lädt
**nichts** neu herunter. Platte anstecken, Ollama neu starten, alles ist da.

**„Öffne mir eine Website" macht jetzt genau das.** Vorher konnte daraus im
Chat eine Bild- oder Video-Erzeugung werden, und Qwirbel drehte sich im Kreis,
bis die CPU heiß lief – dasselbe Muster, das oben beim Work-Tab beschrieben
ist. Der Chat entscheidet jetzt vor allem anderen, dass Nachschauen kein Bauen
ist. Und das Werkzeug zum Aufmachen einer Seite war im Chat **gesperrt**, was
zur Meldung „das würde etwas erstellen – nimm den Work-Tab" führte; eine Seite
aufzumachen erstellt nichts, also ist es jetzt frei. Im Werkzeug-Katalog steht
jetzt auch der Unterschied dabei: eine Seite nur **anzeigen** (dein
Standard-Browser) oder sie **selbst lesen** (über die Browser-Brücke, die
deine Anmeldungen behält).

**Warum Version 2.0.** Damit ist der Stand erreicht, auf den die ganze
1er-Reihe zugelaufen ist: Qwirbel arbeitet an sich selbst (er stellt Sprache,
Modelle, Speicher-Voreinstellungen und Arbeitsweise selbst um, ohne seine
eigenen Grenzen öffnen zu können), er hat sich in dieser Reihe von 67 auf **90
Werkzeuge** gebracht und kann sich bei Bedarf eigene dazubauen, jeder Bereich
ist im Programm einstellbar statt in Dateien, und die Grundregeln, die sich
nicht abschalten lassen, gelten unabhängig von Modell und Anbieter. Neu ist die
Zusage, die vorher nur halb galt: **er nimmt sich deinen Rechner nur, wenn du
ihn dafür benutzt.** Alles läuft weiterhin auf dem eigenen Rechner – auch das
Diktat: die Stimme verlässt den PC nicht.

**Unter der Haube (für die, die es wissen wollen):** 90 Testreihen laufen mit
einem einzigen Befehl durch und sind alle grün. Neu darunter eine Reihe, die
an den echten Netzwerk-Anfragen **nachzählt**, dass beim Start und bei
API-Betrieb wirklich kein lokales Modell angefasst wird – nicht behauptet,
gezählt. Die Endpunkt-Landkarte der eingebauten Dokumentation wird jetzt
automatisch gegen den Code geprüft (204 fehlende Einträge wurden nachgetragen,
jetzt 369 von 369).

## v1.27.0 – Richtig installieren auf Mac und Windows, Bilder per Strg+V, ruhigeres Handy

**Qwirbel installiert sich jetzt wie ein richtiges Programm.**
Auf dem **Mac** genügt nach dem Entpacken ein Doppelklick auf den Installer:
er nimmt die Download-Sperre ab, zieht Qwirbel in den Programme-Ordner
(/Applications) und legt **Qwirbel.app** an — die App erscheint im Launchpad,
lässt sich ins Dock ziehen und meldet sich beim Klick sofort mit
„Qwirbel startet …". Ein zweiter Klick öffnet einfach das laufende Fenster,
statt doppelt zu starten. Auf **Windows** macht
`INSTALLIEREN - Qwirbel (Windows).bat` dasselbe: Installation in die
Programme-Liste, Verknüpfungen auf Desktop und im Startmenü mit Icon, Start
ohne schwarzes Konsolenfenster, Eintrag in „Apps & Features" samt
Deinstallierer. Einen Autostart-Eintrag legt keiner von beiden an — Qwirbel
startet, wenn du es willst. Wer lieber portabel bleibt, nutzt weiter
`setup.bat` bzw. die Terminal-Wege.

**Bilder kommen jetzt per Strg+V in den Chat.** Ein Bild aus der Zwischenablage
(Screenshot, Kopie aus dem Browser) landet direkt in der Eingabezeile – mit
Vorschau vor dem Absenden. Qwirbel speichert es als echte Datei und kann damit
weiterarbeiten (ansehen, bearbeiten, als Video-Startbild). Schlägt das Einfügen
fehl, kommt eine klare Meldung mit Grund statt „unbekannter Fehler".

**Die Spracherkennung ist leichter geworden.** Das Diktat läuft jetzt bevorzugt
über eine schlanke Engine (faster-whisper): braucht ~200 MB statt ~1,5 GB
Arbeitsspeicher und kein torch mehr. Bestehende Installationen laufen unverändert
weiter – die alte Engine bleibt als Rückfallweg. Dazu ein hörbares Feedback,
wenn das Mikrofon an- oder ausgeht.

**Auf dem Handy bleiben keine Hilfe-Kästchen mehr kleben.** Ein Tipp auf eine
Nachricht, den Pfeil-nach-unten oder die Anbieter-Anzeige öffnete die
Maus-Hover-Hilfe – und die blieb stehen, bis man drumherum tippte. Auf
Touch-Geräten erscheinen diese Kästchen jetzt gar nicht mehr; am PC mit Maus
bleibt alles wie gewohnt.

**Kleinigkeit mit Wirkung:** Der Knopf „Zurück an den Platz" an verschobenen
Schwebe-Fenstern zeigt jetzt einen Bogen-Pfeil statt eines Download-Symbols.

## v1.25.0 – Auf dem Mac einfach starten, und Agenten, die wirklich arbeiten

**Auf dem Mac reicht jetzt ein Doppelklick.** Ein Käufer mit einem Mac mini M4
hat uns geschrieben: nach dem Entpacken 28 Ordner, aber keine Datei, die sich
starten lässt – ob das Programm für den Mac überhaupt gedacht sei. Es war
gedacht, die Startdateien lagen nur zwei Ebenen tiefer. Jetzt liegen ganz oben
und der Reihe nach: eine kurze Anleitung, ein Installations- und ein
Startprogramm. Beide öffnen sich per Doppelklick. Der Installierer nimmt dem
Ordner außerdem die Download-Sperre von macOS ab, sodass der Start danach ohne
Umweg funktioniert.

**Werkzeuge, die vorher fehlten.** Qwirbel kann jetzt Dokumente lesen – PDF,
Word, Excel, PowerPoint, OpenDocument und RTF. Ein Vertrag oder eine Rechnung
im Chat ist damit einfach lesbar; ist ein PDF nur ein Scan ohne Textebene, sagt
er das ehrlich, statt sich etwas auszudenken. Dazu kommen: Archive auspacken
(ZIP und TAR), die Zwischenablage lesen und beschreiben, und wiederkehrende
Aufträge selbst anlegen („erinnere mich jeden Montag …").

**„Es ruckelt" genügt.** Sagt man Qwirbel beim Spielen, dass es hakt, stellt er
sich selbst um: er misst erst, bewegt dann genau einen Regler und misst nach.
Last wegnehmen darf er allein – sich mehr Leistung nehmen nur, wenn man es ihm
ausdrücklich sagt. Was er verstellt hat, sagt er, und auf Zuruf dreht er es
zurück.

**Spiele starten wirklich.** „Starte Rocket League" endete früher gern bei
einem YouTube-Video. Qwirbel liest jetzt die Bibliotheken von Steam und Epic
und startet das Spiel über deren Launcher – auch wenn es auf einer anderen
Festplatte liegt. Findet er ein Programm nicht, sagt er das, statt eine
Webseite als Ersatz zu öffnen.

**Die Agenten im Automatik-Tab arbeiten wie im Arbeits-Tab.** Sie liefen bisher
mit angezogener Handbremse und meldeten am Ende „Ziel nicht erfüllt", obwohl
alle Werkzeuge da waren. Jetzt haben sie dieselbe Ausstattung – und man sieht
in der Pixel-Welt, woran sie gerade arbeiten, statt nur „arbeitet …". Läufe,
die ein Neustart unterbrochen hat, werden beim nächsten Start sauber
abgeschlossen; vorher blockierten sie den Job auf Dauer.

**Sicherheit.** Die Datenschutz-Prüfung erkennt Kontonummern jetzt auch mitten
im Satz – vorher rutschte eine IBAN durch, wenn direkt dahinter ein groß
geschriebenes Wort stand. Die Grundregeln, die sich nicht abschalten lassen,
decken zusätzlich ab: heimliche Überwachung, das Nachmachen echter Personen
und gefälschte Ausweise, sowie intime Bilder realer Menschen ohne deren
Einverständnis. Bei Selbstverletzung antwortet Qwirbel nicht mit einer
Verweigerung, sondern verweist auf echte Hilfe. Die Browser-Erweiterung bekommt
Zugriff nur noch auf die Seiten, für die sie gedacht ist.

**MCP-Server werden nicht mehr auf Verdacht gestartet.** Qwirbel merkt sich,
welche Werkzeuge ein Server mitbringt, und startet ihn erst, wenn er ihn
wirklich braucht – vorher liefen bei jeder Nachricht zehn Server kurz mit an.

## v1.24.0 – Menüs, die sitzen, und Schalter, die halten was sie sagen

**Die Auswahl-Menüs sitzen jetzt überall richtig.** Wer die Oberfläche größer
oder kleiner gestellt hat, kannte das: das Menü für Anbieter, Werkzeuge oder
Workflow klappte verschoben auf – manchmal sogar hinter dem Chat, wo kein Klick
mehr ankam. Alle diese Menüs hängen jetzt an einer Stelle im Programm und
sitzen bei jeder Größe genau am Knopf: nachgemessen bei 0,75× bis 1,8×, am PC
wie am Handy. Sie wachsen weiter mit der Oberfläche mit.

**Die Lern-Runde am Chat-Ende bricht nicht mehr ab.** Wenn Qwirbel einen Chat
„durchwirbelt" – zusammenfassen, Erkenntnisse ziehen, Wissen einsortieren,
danach archivieren –, dauert das Minuten. Wurde in dieser Zeit das Fenster neu
geladen oder der Tab gewechselt, blieb die Arbeit auf halber Strecke stehen:
das Wissen war gespeichert, der Chat aber nicht abgeschlossen. Jetzt läuft die
Runde im Hintergrund zu Ende, auch wenn niemand mehr zusieht. Und wenn das
Aufräumen doch scheitert, sagt Qwirbel es, statt „fertig" zu melden.

**Die Oberfläche lädt nicht mehr in laufende Arbeit hinein.** Steht ein Update
bereit, lädt sich das Fenster nach einigen Minuten selbst neu – aber nur noch,
wenn gerade nichts läuft.

**Ein Schalter, der AUS zeigt, ist auch aus.** Der Denken-Schalter wurde vom
Aufwand-Regler überstimmt: bei hoher Stufe dachte das Modell weiter, obwohl der
Schalter unten stand. Jetzt entscheidet der Schalter, der Regler darf nur noch
innerhalb von „an" sparsamer werden.

**Kleinigkeiten, die man täglich sieht.** Die Anzeige beim Bilder- und
Video-Erzeugen wächst nicht mehr mit dem Timer, sondern zeigt einen echten
Fortschrittsbalken – und wo die Dauer unbekannt ist, wird keine Prozentzahl
erfunden. Im langen Chat gibt es neben den Kapiteln jetzt auch einen Pfeil
zurück an den Anfang.

**Für Workflows denkt Qwirbel jetzt an deine Grafikkarte.** Er misst, was
wirklich verbaut ist, sagt es dir im Klartext und leitet daraus die Grenzen ab –
statt Modelle vorzuschlagen, die auf deiner Karte gar nicht laufen.

## v1.23.0 – Einstellungen, die bleiben, und ein Programm, das dir gehört

**Deine Einstellungen bleiben jetzt wirklich.** Farben, Tab-Farben, die Größe
der Oberfläche, dein ausgeblendetes Menü – all das war nach einem Neustart im
Programmfenster manchmal wieder weg. Die Ursache lag tief (das Fenster hatte
keinen festen Speicher) und ist behoben: einmal eingestellt, bleibt es. Eine
selbst gewählte Tab-Farbe gewinnt außerdem gegen die globale Akzentfarbe.

**Ein Hintergrund nach deinem Geschmack.** Unter Darstellung wählst du jetzt,
wie der ganze Hintergrund aussieht: die schwebenden Symbole wie bisher, ganz
schlicht, das Maskottchen, das zu deinem Mauszeiger schaut – oder dein eigenes
Bild mit einem Weichzeichner-Regler, damit der Text lesbar bleibt. Dazu ein
heller Modus für alle, die es freundlicher mögen.

**Qwirbel auf jedem Gerät im selben Chat.** Wenn der PC gerade an einer Antwort
arbeitet, siehst du das jetzt auch auf dem Laptop oder Handy im selben Chat –
mit einem Stopp-Knopf, der von überall wirkt. Und Stoppen geht sofort, statt
wie früher kurz zu hängen.

**Von anderen Geräten verbinden – ein Doppelklick.** Im Paket liegt eine
kleine Verbinden-Datei für Windows und Linux: einmal die Adresse deines PCs
eintragen (im WLAN oder über einen sicheren Tunnel von unterwegs), danach
genügt ein Doppelklick, um Qwirbel auf dem Laptop zu öffnen.

**Sicherer im Netz.** Qwirbel führt beim Surfen keine aus dem Internet
geladenen Befehle mehr aus – ein Muster, das Virenscanner zu Recht anspringt.
Das war noch nie nötig und ist jetzt fest ausgeschlossen.

## v1.22.0 – Recherche, Videoschnitt und ein aufgeräumtes Gedächtnis

**Qwirbel recherchiert jetzt selbst.** Sag ihm ein Thema, und er sucht im Netz,
liest mehrere Seiten und schreibt dir daraus ein sauberes Recherche-Dokument –
jede Aussage mit ihrer Quelle belegt, Unsicheres ehrlich markiert, die Quellen
mit Datum am Ende. Kein Copy-Paste-Wust mehr, sondern eine fertige Zusammenfassung.

**Videos schneiden – einfach im Chat.** „Schneide die ersten drei Sekunden weg",
„häng die beiden Clips zusammen", „zieh ein Standbild raus" oder „mach das kleiner"
gehen jetzt als Werkzeug. Auch Clips mit unterschiedlicher Größe werden sauber
zusammengefügt, statt mit einer Fehlermeldung abzubrechen.

**Jeder Agent zeigt, woran er arbeitet.** Wenn mehrere Agenten gleichzeitig für
dich arbeiten, hat jetzt jeder sein eigenes Aufgaben-Fenster – aufklappbar, mit
Haken und laufenden Werkzeugen. Und der Aufseher-Modus (Qwirbel wird die „Mama"
und wacht über die Helfer, statt selbst mitzubauen) lässt sich im GO-Dialog
an- und ausschalten.

**Ein Chat, der mitwächst.** Scrollst du in einem langen Gespräch nach oben,
fliegt eine Leiste ein – mit deinen eigenen Beiträgen als Kapitel, zu denen du
direkt springen kannst, plus Export/Löschen/QWIRBELN immer griffbereit.

**Wissen, das nicht mehr ausufert.** Der QWIRBELN-Knopf im Wissen-Tab sammelt
dein Wissen nicht mehr in hunderte Dateien, sondern arbeitet es in **20 feste
Kern-Dateien** ein (Personen, Hardware, Programme, Projekte … plus eine kreative).
Einmal drücken, bis „alles eingearbeitet" dasteht – der Rest bleibt übersichtlich.

**Rechtsklick, wie man es kennt.** Auf dem Eingabefeld, in jedem Textfeld und auf
Chat-Nachrichten gibt es jetzt ein eigenes Rechtsklick-Menü im Qwirbel-Look:
Ausschneiden, Kopieren, Einfügen, Alles auswählen – und bei Nachrichten zusätzlich
Zitieren und „genauer erklären lassen".

**Unter der Haube:** Qwirbels eingebaute Ethik gilt jetzt wirklich auf **jedem**
Weg – auch bei der Web-Recherche, beim Zusammenfassen und in jedem Agenten-
Schritt. Und Qwirbel darf sich seine eigenen Grenzen weiterhin nicht selbst
aufmachen.

## v1.21.0 – Der Schwarm wird richtig geführt

**Erst bauen, dann prüfen – die Agenten laufen jetzt in Wellen.** Bisher legten
alle Helfer gleichzeitig los, auch der, der am Ende testen sollte: Er prüfte
Dateien, die es noch gar nicht gab. Jetzt bekommt jeder Teilauftrag eine Phase –
**bauen**, **zusammenfügen**, **prüfen & dokumentieren**. Eine Welle startet erst,
wenn die vorherige durch ist; innerhalb einer Welle läuft weiter alles parallel.
Und wenn ein Auftrag nach Testen klingt, rutscht er automatisch nach hinten –
auch dann, wenn er als „unabhängig" angekündigt wurde.

**Ein echter GO-Knopf.** Fragt Qwirbel, ob er einen Schwarm starten soll, stellst
du in Ruhe zusammen, womit gearbeitet wird: **mehrere Anbieter gleichzeitig**
(lokal *und* GLM *und* Gemini – ihre Kontingente addieren sich, du siehst sofort
„max 14 gleichzeitig"), dazu wie viele Agenten. Erst dein Druck auf **GO** schickt
sie los. Vorher startete schon der Klick auf eine Zahl, und ein getipptes „go"
landete als neue Aufgabe im Chat, statt die Frage zu beantworten – das geht jetzt
beides: Knopf oder einfach „go" schreiben.

**Qwirbel wird wirklich die Mama.** Hat er Helfer losgeschickt, baut er ihre Teile
nicht mehr selbst nach. Er wartet mit einem eigenen Werkzeug auf sie, meldet sich,
sobald etwas passiert, greift bei Fehlern ein – und kann seine Aufgabe erst dann
abschließen, wenn wirklich alle durch sind. Danach sieht er selbst nach, ob die
Dateien da sind und ob es baut.

**Ein Haken ist kein Beweis.** Steht in einer Roadmap „✅ erledigt", zählt das für
Qwirbel nicht mehr als Nachweis – er prüft die Dateien selbst. Vorher konnte es
passieren, dass er „erledigt und verifiziert" meldete, während in Wahrheit nichts
da war.

**Gezeigte Bilder kommen an – und bleiben.** Wenn Qwirbel dir etwas zeigt,
erscheint es sofort als eigene Zeile im Chat, auch wenn die Aufgabe im Hintergrund
weiterläuft oder du auf dem Handy schaust. Nach einem Neuladen ist es immer noch da.

**Bilder anklicken verliert nichts mehr.** Ein Klick öffnet das Bild jetzt groß im
Fenster (Esc oder Klick schließt) statt die Seite zu verlassen – vorher waren
danach die Anhänge der Nachricht weg.

**Lange Befehle halten Qwirbel nicht mehr auf.** Läuft ein Upload, ein Build
oder ein Render, wartete er bisher im Werkzeug – der nächste Schritt stand
schon fest und passierte trotzdem nicht. Jetzt übergibt er solche Läufe nach
gut einer Minute an den Hintergrund (**nichts wird abgebrochen**), arbeitet
weiter und holt sich das Ergebnis später mit einem eigenen Werkzeug.

**Er verliert den Faden nicht mehr, wenn du dazwischenredest.** Schreibst du
mitten in der Arbeit etwas dazu, sagt er kurz *„Habe ich notiert – ich mache
erst X fertig, dann kümmere ich mich darum"*, führt den laufenden Schritt sauber
zu Ende und nimmt deinen Wunsch danach dran. Eine echte Korrektur („stopp",
„nein, anders") gilt weiterhin sofort.

**Das Ansicht-Fenster zeigt endlich, was er sieht.** Ist die Browser-Erweiterung
gekoppelt, kommt das Bild aus **deinem** Browser – vorher fragte diese Ansicht
stur einen eigenen, den es gar nicht gibt, und blieb leer, während Qwirbel
sichtbar arbeitete. Das Fenster lässt sich außerdem **frei verschieben**
(am Kopf greifen, Doppelklick setzt es zurück).

**Das richtige Logo in der Taskleiste.** Windows zeigte für Qwirbel bisher das
Python-Symbol; jetzt steht dort – und im System-Tray – das Maskottchen.

**Ein Werkzeugkasten an Kurzbefehlen für Work & Code.** `/bau`, `/fix`, `/test`,
`/build`, `/erklaer`, `/refactor`, `/review`, `/doku`, `/ordner`, `/finde`,
`/starte`, `/agenten`, `/lage`, `/schnitt`, `/aufraeumen` – dazu `/musik` und
`/zeig`. Tippe **/** und das Menü schreibt den Satz vor. `/hilfe` erklärt alles
nach Themen sortiert, und Qwirbel selbst kann die Befehle erklären.

**Das Ansicht-Fenster ist nicht mehr leer.** Auch ohne verbundenen Browser steht
dort jetzt, was Qwirbel gerade tut: aktueller Schritt, laufende Handlung und wie
viele Schritte erledigt sind. Der lange Kopplungs-Hinweis ist auf einen Satz
gekürzt.

## v1.20.0 – Ein Schwarm, der wirklich zusammenarbeitet

**Mehrere Helfer gleichzeitig – der neue Agentic-Tab.** Große Aufträge zerfallen
in Teile, die nichts voneinander brauchen. Genau die bekommen jetzt jeder ihren
eigenen Agenten: eine Zeile ist ein Auftrag, alle laufen parallel, jeder mit
eigener Farbe, eigenem Leuchtpunkt und einem aufklappbaren Fenster, in dem steht,
woran er gerade sitzt. Oben siehst du auf einen Blick, wie viele arbeiten,
warten und fertig sind – mit „Alle stoppen" und „Aufräumen".

**Qwirbel erkennt selbst, wann es groß wird, und fragt nach.** Nennst du ein
Projekt, schaut er wirklich nach: Gibt es dort eine Roadmap (PROJEKT.md, einen
Bauplan)? Wie viele Dateien liegen schon da? Nennst du mehrere Dinge auf einmal?
Passt das zusammen, fragt er einmal kurz: *Soll ich dafür mehrere Agenten
gleichzeitig arbeiten lassen?* – du wählst den Anbieter und wie viele (10, 20,
30 oder „Qwirbel entscheidet"), oder sagst Nein, dann macht er es allein. Die
Teilaufträge liest er aus deiner Roadmap, statt sie sich auszudenken.

**Er passt auf deine Maschine auf.** Eine Grafikkarte kann nur eines auf einmal:
* **Nur noch ein Bild-/Video-Auftrag zur selben Zeit.** Vorher konnten sich zwei
  Läufe in die Quere kommen – einer räumte den Speicher frei, während der andere
  noch rechnete. Jetzt wartet der zweite ordentlich, sichtbar, mit Ansage.
* **Lokal denken höchstens zwei Agenten gleichzeitig** (sie teilen sich ja eine
  Karte), über einen Cloud-Anbieter dürfen es viele sein. Das entscheidet
  Qwirbel selbst, du musst nichts einstellen.
* **Kein zweiter Schwarm nebenher.** Läuft schon einer, wird ein zweiter
  abgelehnt – zwei Gruppen an denselben Dateien schreiben sich gegenseitig kaputt.
* **Programme werden nicht doppelt gestartet.** Läuft Unity schon, arbeitet er
  mit dem offenen Fenster weiter, statt ein zweites aufzumachen.
* **Neu: „Wie ist die Lage?"** Qwirbel kann jetzt in einem Zug nachsehen, wie
  viel Grafikspeicher frei ist, ob gerade etwas generiert wird, ob du im
  Vollbild spielst und wie viel Platz die Platte hat – und danach handeln,
  statt zu fragen.

**Fest eingebaute Grundregeln – in jedem Modell, auf jeder Filterstufe.** Qwirbel
hat jetzt einen Grundschutz, der sich nicht abschalten lässt und auch dann gilt,
wenn der Inhaltsfilter auf „keine" steht oder ein fremdes Modell geladen ist:
keine Hilfe beim Angriff auf fremde Konten, Geräte, Netzwerke oder Bankzugänge,
keine Waffen- oder Sprengstoff-Anleitungen, kein Beleidigen, Bedrohen oder
Ausspähen echter Menschen, und niemals sexuelle Inhalte mit Minderjährigen.
Solche Bitten werden freundlich, aber klar abgelehnt – mit einem Hinweis, was
stattdessen geht (die eigenen Geräte absichern, verstehen wie Angriffe laufen,
Hilfe wenn man selbst betroffen ist). Was erlaubt bleibt, bleibt erlaubt: der
Filter für alles andere ist weiter deine Entscheidung.

**Der Chat vergisst nichts mehr, wenn du das Fenster zumachst.**
* Schließt du die App, während eine Aufgabe läuft, arbeitet sie weiter – und ihr
  **Ergebnis landet jetzt auch wirklich im Verlauf**. Vorher ging es verloren,
  und im Aufgabenfenster blieb eine Geisteraufgabe stehen.
* Kommt das Fenster zurück, holt sich Qwirbel sofort den echten Stand: laufende
  Aufgaben, Timer und die Chats laden frisch nach – auch nach einem Neustart.
* **„Er meldet sich"** kommt zuverlässig an. Seine Zwischenrufe liefen bisher nur
  über eine einzige Leitung; brach die weg, war die ganze Erzählung weg. Jetzt
  gibt es einen zweiten Weg – und nichts steht doppelt da.
* **Der Ladekreis bleibt nicht mehr hängen**, wenn Qwirbel zwischendurch laut
  mitdenkt.
* Bei zwei gleichzeitigen Aufgaben landet die **Rückfrage im richtigen Chat**.

**Ein Bild im Work- oder Code-Tab ist jetzt Zusatzwissen, kein Auftrag.** Schick
einen Screenshot mit „bau mir was dazu": Qwirbel sieht ihn sich an, beschreibt
ihn für sich und baut damit weiter. Vorher wurde daraus entweder ein Video oder
nur eine Bildbeschreibung – und dein eigentlicher Auftrag fiel unter den Tisch.
Im normalen Chat bleibt alles wie gewohnt.

**Bild-Bearbeitung mit bis zu drei Bildern.** Wähle einen Image-Edit-Workflow
und du bekommst drei Felder: Bild 1 ist das, was bearbeitet wird (es gibt Größe
und Format vor), Bild 2 und 3 sind optionale Vorlagen – „nimm die Jacke aus Bild
2". Lässt du Felder leer, werden die im Workflow sauber abgehängt; vorher brach
die Generierung ab oder es wurde still dasselbe Bild doppelt verwendet. Nebenbei
behoben: zwei verschiedene Bilder konnten beim Hochladen denselben Dateinamen
bekommen und sich überschreiben – mit einem Bild fiel das nie auf, mit dreien
sofort.

**Qwirbel kann sich selbst einrichten.** Sag einfach, was anders sein soll –
„antworte auf Englisch", „nimm ein anderes Standardmodell", „entlade nach dem
Bild alles", „mach die Videos schneller" – und er stellt es um, statt dir zu
erklären, in welchem Menü das steht. Er kann sich auch ein fehlendes Modell
nachziehen und einen ComfyUI-Workflow übernehmen, den du ihm gibst. Was er
NICHT selbst darf, ist Absicht: seine eigene Autonomie-Stufe, den Inhaltsfilter,
Lizenz, Passwörter und Rechte ändert weiterhin nur du. So wächst er mit, ohne
sich selbst die Grenzen aufzumachen.

**Mehrere KI-Anbieter gleichzeitig – und Ollama abwählbar.** Im Agentic-Tab
hakst du an, wo gedacht werden soll: lokal (2 Plätze), GLM (6), Gemini (6) –
die Plätze addieren sich, hier also 14 Agenten gleichzeitig. Wählst du „Lokal"
ab, bleibt deine Grafikkarte komplett frei und du kannst nebenher zocken.
**Fällt ein Anbieter aus, wird sein Auftrag automatisch bei einem laufenden
nachgetragen** – nichts bleibt liegen, und der ausgefallene wird dabei
übersprungen.

**Er flasht dir nichts mehr über das Vollbild.** Startet Qwirbel ein Programm,
während du im Vollbild spielst oder ein Video schaust, öffnet es sich
**minimiert** statt dir den Bildschirm wegzureißen. Neu kann er Fenster auch
in Größe und Position bringen oder **auf einen anderen Monitor schieben** –
ohne sie nach vorn zu holen.

**Vorschläge passen jetzt zum Thema.** Die Eingabe-Hilfe schlug früher gern
„für Paper 1.21" vor, auch wenn es um Roblox, ein Video oder eine Tabelle
ging. Und wenn du „arbeite an Projekt X" gesagt hast, hat er manchmal über
einen ganz anderen Ordner geredet – er nimmt jetzt den Ordner, den DU nennst,
statt einfach den Arbeitsordner.

**Kleinigkeiten, die im Alltag zählen**
* **Bis zu 25 Anhänge** pro Nachricht statt 10.
* **Ein „UI"-Knopf** neben „VRAM freigeben" lädt die Oberfläche neu – praktisch
  im Programmfenster, wo es kein F5 gibt.

## v1.19.0 – Er bleibt beim Schritt, und dein Schreibschutz gilt

**Schritt für Schritt heißt jetzt wirklich Schritt für Schritt.** Der Plan
startete zwar mit einem Schritt – danach durfte Qwirbel sich aber selbst eine
neue Liste mit mehreren Punkten schreiben und stand wieder da, wo er vorher
war. Zwei Löcher waren schuld, beide sind zu:

* **Umplanen ergibt höchstens einen neuen Schritt.** Schickt das Modell drei,
  wird der erste genommen und der Rest verworfen – mit dem klaren Hinweis, den
  nächsten erst anzuhängen, wenn das Ergebnis des aktuellen dasteht.
* **Ein Schritt darf nur einmal umgeplant werden.** Vorher konnte Qwirbel im
  selben Schritt mehrfach hintereinander umplanen, ohne je etwas zu tun – der
  Schritt wurde nie fertig und wurde auch nie abgehakt. Nach dem ersten Mal
  zählt nur noch, was er wirklich tut.
* **Keine zusammengesetzten Schritte mehr.** „Datei suchen, dann die Regeln
  laden" sind zwei Schritte, nicht einer. Die Anleitung sagt das jetzt mit
  einem Beispiel, statt es nur zu umschreiben.

**Schreibgeschützte Dateien bleiben schreibgeschützt.** Wer eine Datei bewusst
sperrt, will nicht, dass ein Automat sie wieder aufmacht. Bisher bekam Qwirbel
nur ein nacktes „Permission denied" und wusste damit nichts anzufangen – er
probierte es erneut oder blieb hängen, und dein Schutz sah aus wie ein Fehler
im Programm. Jetzt sagt er klar, dass die Sperre Absicht ist, fasst die Datei
nicht an und schlägt vor, eine neue daneben zu schreiben. **Lesen und
Ausführen gehen unverändert** – gesperrte Skripte lassen sich also weiterhin
ganz normal starten. Den Schutz aufheben kannst nur du, von Hand.

## v1.18.0 – Er denkt jetzt Schritt für Schritt (und hat Hände)

**Qwirbel plant nicht mehr fünf Schritte ins Blaue.** Bisher stand der ganze
Plan fest, bevor der erste Schritt getan war. Manche Modelle erledigen dann den
kompletten Auftrag gleich im ersten Schritt – und arbeiten die restlichen
trotzdem ab. Das Ergebnis war alles doppelt: doppelte Dateien, doppelte Videos,
doppelte Rechenzeit. Jetzt entsteht **ein** Schritt, er wird getan, das
Ergebnis wird angesehen – und daraus ergibt sich der nächste. Das
Aufgaben-Fenster bleibt genau wie es war; die Liste wächst nur mit der Arbeit,
statt vorher erfunden zu werden.

* **Maus und Tastatur** – Qwirbel konnte schon sehen, jetzt kann er auch
  anfassen. Er bedient Programme, die keine Kommandozeile haben: Installer,
  Dialoge, Launcher. Der Ablauf ist fest vorgegeben: hinsehen, klicken,
  **nochmal hinsehen** – ein abgeschickter Klick gilt ihm nicht als Beweis.
  Wie beim Klicken auf Webseiten fragt er unterhalb der höchsten
  Autonomie-Stufe vorher nach.
* **Fernsteuerung vom Handy läuft jetzt auf allen drei Systemen.** Sie hing
  bisher an einer Linux-Schnittstelle – auf Windows und macOS passierte beim
  Tippen schlicht nichts. Ohne zusätzliche Installation.
* **Er merkt sich Gespräche.** Was in früheren Chats entschieden wurde, findet
  er von selbst wieder – passend zur aktuellen Frage. Und innerhalb eines
  langen Gesprächs bleiben deine Vorgaben von ganz oben gültig, auch wenn sie
  längst aus dem Sichtfeld gerutscht sind.
* **Qwirbeln im Wissen-Tab** – ein Knopf fasst dein gesammeltes Wissen zu einem
  Überblick zusammen und legt ihn als **neue** Datei ab. Nichts wird
  überschrieben. Welches Modell das macht, wählst du: lokal oder ein
  Anbieter deiner Wahl. Auch das Qwirbeln im Chat kann das jetzt.
* **Tipps beim Tippen** haben endlich eine Einstellung: an/aus, welches Modell,
  ab wie vielen Zeichen, wie lange gewartet wird. Fehlt das gewählte Modell,
  nimmt Qwirbel ein vorhandenes – und **sagt das auch**, statt stillschweigend
  nichts mehr vorzuschlagen.
* **Neue Werkzeuge**: PowerShell, Löschen (durch dieselbe Sicherheitsabfrage
  wie alles andere), mehrere Stellen einer Datei in einem Zug ändern,
  Notizen ins Wissen schreiben, Termine und Aufgaben wirklich eintragen,
  deine ComfyUI-Standards nachschlagen, Modelle auflisten, Grafikkarte
  freiräumen. Sag ihm „trag mir Freitag 15 Uhr Zahnarzt ein" – jetzt steht es
  auch drin.
* **Ergebnis auf einen Blick**: Am Ende einer Aufgabe steht über dem Bericht,
  wie lange es gedauert hat, wie viele Schritte und Züge es waren und was
  entstanden ist. Fehlgeschlagene Züge werden dabei **nicht** versteckt.
* **Der MCP-Tab flackert nicht mehr.** Die Liste der installierten Server baute
  sich bei jeder Kleinigkeit neu auf – beim Eintippen eines Schlüssels ging
  dabei sogar der Cursor verloren.
* **Die Knopfleiste im Chat ist aufgeräumt.** Bei schmalerem Fenster
  brachen die Knöpfe in drei krumme Zeilen um und die Token-Anzeige klebte
  mitten in den Chips. Jetzt: eine Zeile, wenn Platz ist – sonst zwei saubere
  Reihen (Einstellungen oben, Aktionen unten). Gemessen wird die Breite der
  Chat-Spalte, nicht die des Fensters; genau daran war es vorher gescheitert.
* **Handy-App aufgefrischt.** Das App-Symbol war noch das alte: Android hat es
  rund zugeschnitten, wodurch der Schriftzug abgeschnitten wurde und das
  Motiv winzig war. Neu ist ein richtiges adaptives Symbol – Motiv frei
  gestellt, Verlaufs-Hintergrund, dazu die einfarbige Variante für Androids
  Themed Icons. Die App zeigt jetzt außerdem dieselbe Versionsnummer wie
  Qwirbel selbst (vorher stand dort dauerhaft „1.0").
* **Neu: iPhone-/iPad-App.** Vollständiger Quellcode im Ordner `ios-app`
  samt Installationsanleitung – QR-Kopplung, Adresse merken, Herunterziehen
  zum Neuladen, ehrlicher Fehler-Bildschirm. Zum Bauen ist ein Mac mit Xcode
  nötig (Apples Regel, nicht unsere); die Anleitung nennt die drei Wege aufs
  Gerät samt Kosten und Laufzeit.
* **Bewegungs-Übertragung (Motion-Control) ist jetzt eingebaut.** Ein
  Referenzbild sagt WER, ein Video sagt WIE – beides lässt sich reinziehen,
  auswählen oder als Pfad einfügen (praktisch bei Clips, die schon auf der
  Platte liegen). Qwirbel prüft vorher, ob das Video überhaupt so lang ist wie
  gewünscht, und sagt es, statt still zu kürzen.
* **Verrauschte Videos behoben.** Die Bildanzahl muss bei diesen
  Video-Modellen auf ein bestimmtes Raster passen (4·n+1). Traf sie das nicht –
  bei 5 Sekunden × 15 Bildern/s zum Beispiel – liefen Bild-Vorgabe und
  Zeitachse auseinander, und das Ergebnis sah aus, als hätte die
  Beschleunigungs-LoRA nicht gegriffen. Qwirbel zieht die Anzahl jetzt selbst
  auf den nächsten gültigen Wert. **Bild-Erzeugung und Bild-Bearbeitung sind
  davon nicht berührt** und bleiben unverändert schnell.
* **Fehlende LoRA-Dateien werden erkannt.** Stand in einem Workflow eine LoRA
  eingeschaltet, deren Datei anders heißt, lief die Erzeugung scheinbar durch –
  nur eben ohne sie, also mit Rauschen. Jetzt sucht Qwirbel die passende Datei
  und sagt, wenn er sie ersetzt hat; findet er keine, bricht er vorher ab
  statt 45 Minuten für ein unbrauchbares Video zu rechnen.
* **Zahnrad an der Eingabe.** Über das Zahnrad rechts lässt sich einzeln
  festlegen, welche Schalter unter dem Eingabefeld überhaupt erscheinen –
  Token-Zähler, Mikrofon, Vorlesen, Werkzeuge und so weiter. Was weg ist,
  macht Platz, die Zeile rückt sauber zusammen. Senden und Stop bleiben immer.
* **Profil beim Einrichten.** Ganz am Anfang fragt Qwirbel jetzt, wofür du
  ihn hauptsächlich benutzen willst – *Einfach*, *Arbeit*, *Kreativ* oder
  *Alles*. Danach steht nur da, was dazu passt: aus 20 Bereichen werden bei
  *Einfach* sieben, und die Schalter unter der Eingabe schrumpfen mit.
  Es geht nichts verloren – *Alles* holt jederzeit alles zurück, und unter
  Einstellungen → Menü lässt sich jeder Bereich einzeln wieder einblenden.
* **Fertige Farb-Themes.** Unter Darstellung stehen acht abgestimmte Themes
  (Qwirbel, Mitternacht, Terminal, Bernstein, Magenta, Türkis, Rost, Eis).
  Ein Klick setzt Akzent, Hintergrund und Felder gemeinsam – und weil danach
  genau diese drei Werte in den Reglern darunter stehen, sieht man, woraus
  ein Theme besteht, und kann sich daraus sein eigenes bauen.
* **Aufklapp-Menüs bleiben im Bild.** Die Menüs der rechten Schalter klappten
  nach rechts auf und schoben sich bei schmalerem Fenster aus dem Bild.
* **Behoben**: In unbeaufsichtigten Abläufen wurde „läuft ComfyUI überhaupt?"
  fälschlich als heikle Handlung eingestuft und blockiert – damit stand dort
  jede Generierung. Das mitgelieferte Kubernetes-Paket nannte außerdem eine
  veraltete Versionsnummer.

**Für Firmen-Kunden wichtig:** Ein Mitarbeiter-Konto konnte über zwei
Lese-Werkzeuge **Dateien außerhalb des eigenen Arbeitsbereichs** einsehen –
auch die anderer Konten. Die Ursache war eine Lücke in der Zuordnungstabelle,
nicht in der Logik. Sie ist geschlossen; zusätzlich prüft eine Testreihe jetzt
**jedes** Werkzeug und schlägt an, sobald eines ohne Begrenzung dazukommt.
Maus, Tastatur, PowerShell, Bildschirm und Grafikkarte sind für
Mitarbeiter-Konten grundsätzlich gesperrt – sie wirken auf dem Server, nicht
am eigenen Platz. **Bitte zeitnah aktualisieren.**

## v1.17.0 – Browser-Brücke statt Fernsteuerungs-Port

**Qwirbel startet oder beendet deinen Browser nie mehr.** Der alte Weg
verlangte einen Browser-Neustart mit Fernsteuerungs-Port – dabei ging die
Sitzung verloren und man war anschließend aus allen Konten ausgeloggt. Der
einzige Weg zum Browser ist jetzt die mitgelieferte **Erweiterung**, die im
laufenden Fenster sitzt: kein Neustart, keine verlorenen Anmeldungen.

* **Browser-Brücke** – Erweiterung liegt im Ordner `browser-extension` samt
  Anleitung (`LIES_MICH.md`, deutsch + englisch). Einrichtung: Erweiterungs-
  Seite öffnen, Entwicklermodus an, Ordner laden. Sie meldet sich von selbst
  an; ein Kopplungs-Code ist nur im strengen Modus nötig.
  Status jederzeit unter **Einstellungen → Verbindung → Browser koppeln**.
* **Sicherheit** – Befehle, die einen Browser beenden oder mit
  Fernsteuerungs-Flags starten, werden hart blockiert. Das gilt auf jeder
  Autonomie-Stufe und lässt sich nicht per Einstellung abschalten.
* **VRAM freigeben** sagt jetzt die Wahrheit: nach dem Entladen wird
  nachgesehen. Liegt ein Modell noch im Speicher, weil eine laufende Aufgabe
  es sofort nachlädt, steht genau das da – statt einer Erfolgsmeldung.
* **Stop-Knopf** beendet einen Chat-Lauf wirklich: laufende Modell- und
  Anbieter-Verbindungen werden geschlossen, sofern kein zweiter Chat arbeitet.
* **Zwischennachrichten** im Chat erscheinen nur noch einmal. Sie rücken an
  die Stelle, an der die KI sie gelesen hat, statt doppelt dazustehen.
* **Ansicht-Feld** (früher „Browser") zeigt jedes Werkzeug, das Qwirbel
  gerade benutzt – auch wenn er ein Programm öffnet, nicht nur Webseiten.

# Qwirbel – Änderungsverlauf

## v1.16.0 (Qwirbel benutzt deinen ganz normalen Browser)

**Endlich: dein Browser, deine Anmeldungen – ohne Neustart, ohne Extra-Profil.**
Bisher musste der Browser für Automatisierung mit einem Debug-Schalter neu
gestartet werden. Das hieß: Browser schließen, Sitzung riskieren, im
schlimmsten Fall überall ausgeloggt. Jetzt gibt es eine **Browser-Erweiterung**,
die im bereits laufenden Browser sitzt. Qwirbel schickt ihr Befehle, sie führt
sie im normalen Fenster aus – mit genau den Anmeldungen, die ohnehin offen
sind. Kein Neustart, kein zweites Profil, kein erneutes Einloggen. Funktioniert
in Chrome, Brave, Edge, Opera, Opera GX und Vivaldi.

**Einmal koppeln, dann nie wieder.**
In den Einstellungen erzeugt Qwirbel einen kurzen Code, der einmal in die
Erweiterung eingegeben wird. Danach merkt sie sich ein dauerhaftes Token –
auch über Neustarts von Programm und Rechner hinweg. Der Code ist nötig, weil
sonst jede beliebige Webseite eine lokale Verbindung aufmachen und den Browser
fernsteuern könnte.

**Was die Erweiterung NICHT tut:** Sie liest keine Cookies aus, verschickt
nichts ins Internet und spricht ausschließlich mit Qwirbel auf demselben
Rechner. Läuft Qwirbel nicht, tut sie gar nichts.


## v1.15.0 (Man sieht ihm bei der Arbeit zu – und die Grafikkarte bleibt frei)

**Im Chat steht jetzt, was er wirklich anfasst.**
Bisher liefen die Arbeitsschritte nur im Live-Panel: nach einem Neuladen waren
sie weg, auf einem zweiten Gerät kamen sie nie an, und wer die Aufgabe nicht
selbst gestartet hatte, sah gar nichts. Jetzt landet jede verändernde Handlung
als eigene Zeile im Verlauf – „ändert GameManager.cs +42 −3", „packt
paket.zip 12 MB", „kompiliert". Reines Lesen bleibt bewusst draußen, sonst
wäre der Verlauf nur noch Lärm.

**Neu: Knopf „VRAM freigeben".**
Unten links, direkt unter der Ollama-Anzeige. Wirft alle geladenen lokalen
Modelle aus dem Grafikspeicher und stoppt die lokale Engine – **ohne** laufende
Aufgaben abzubrechen, im Gegensatz zum großen Stop-Knopf. Hintergrund: ein
geladenes Modell belegt Speicher, auch wenn es gerade nichts rechnet (gemessen:
ein 12B-Modell = 7,3 GB im Leerlauf). Wer nebenher spielt oder Bilder
generiert, braucht diesen Platz. ComfyUI wird nur auf ausdrücklichen Wunsch
mitgenommen, weil dort meist eine halbfertige Generierung dranhängt.

**Behoben: bei Cloud-Aufgaben sprang trotzdem ein lokales Modell an.**
Am Ende **jeder** Aufgabe lief der Lern-Schritt („was ist die wichtigste
Erkenntnis?") hart über ein lokales Modell – auch wenn die komplette Aufgabe
über einen Cloud-Anbieter lief. Auf einer 16-GB-Karte, auf der nebenbei ein
Spiel läuft, merkt man genau das. Jetzt lernt der, der auch gearbeitet hat.

**Behoben: er hat trotz höchster Autonomie-Stufe nachgefragt.**
Zwei getrennte Ursachen. Erstens brauchte das Überschreiben bestehender
Dateien außerhalb des Arbeitsordners weiterhin einen Klick – auf Stufe 5, wo
ausdrücklich alles freigegeben ist, ist das ein Widerspruch; dort ist
Überschreiben im eigenen Benutzerordner jetzt frei (Systembereiche bleiben
hart gesperrt). Zweitens gibt es jetzt einen Schalter, der auf Stufe 5
automatisch greift: **keine Rückfragen mehr**, weder als Fenster noch als
Frage im Text. Fehlt etwas, nimmt er die sinnvollste Variante und schreibt am
Ende dazu, was er angenommen hat.

## v1.13.0 (Erst schauen, dann planen – und man sieht ihm beim Arbeiten zu)

**Er schaut sich erst um, bevor er einen Plan macht.**
Bisher entstand der Plan blind: Qwirbel wusste beim Planen weder, wie das
Projekt aufgebaut ist, noch welche Programme auf dem Rechner überhaupt
installiert sind. So kam es zu Plänen, die von der ersten Zeile an nicht
passten – zum Beispiel ein Python-Plan für ein Projekt, das in Wahrheit aus
C#-Dateien besteht, oder ein „App bauen"-Schritt, obwohl das nötige Bau-Werkzeug
gar nicht da ist. Jetzt sieht er sich **vor** dem Planen den Projektordner an
(Struktur, wo der Quellcode wirklich liegt, welche Dateitypen es gibt) und
prüft, welche Bau-Werkzeuge und Programme wirklich vorhanden sind. Dieser
Befund steht im Plan und in jedem Arbeitsschritt – und was dort nicht steht,
hat der Rechner nicht. Fehlt etwas, sagt er es, statt es zu planen.

**Er plant sich Schritt für Schritt selbst weiter.**
Statt einen langen Plan ins Blaue zu schreiben, plant er den Anfang genau und
hängt danach jeden weiteren Schritt selbst an – zusammen mit einer Notiz an
sich selbst, was dieser Schritt wissen muss (echte Pfade, was schon
funktioniert hat, welche Stolperfalle es gab). Beim letzten Schritt der Liste
weiß er jetzt auch, dass er weitermachen soll, wenn das Ziel noch nicht
erreicht ist – vorher blieb er dort einfach stehen.

**Sparsam lesen statt ganze Dateien verschlingen.**
Zwei neue Werkzeuge: eine Suche **im Inhalt** aller Projektdateien (Datei +
Zeilennummer als Ergebnis) und ein **Ausschnitt-Leser**, der nur die
gewünschten Zeilen holt – mit Zeilennummern und der Angabe, wie lang die Datei
insgesamt ist. So arbeitet er in großen Projekten gezielt, statt sich mit
tausenden Zeilen zuzuschütten, die er gar nicht braucht. Das macht ihn
schneller, günstiger und vor allem genauer.

**Man sieht im Chat, was er tut – Zeile für Zeile.**
Neu ist eine mitlaufende Gedankenkette im Chat: jeder Handgriff erscheint als
eigene Zeile, mit Haken wenn er geklappt hat. Dabei stehen jetzt auch die
Zahlen dahinter – **+42 −3** bei geänderten Dateien, „7 Treffer in 3 Dateien"
bei einer Suche, „Zeile 96–140 von 450" bei einem Ausschnitt. Und der
Warte-Kreis sagt nicht mehr immer nur „Qwirbel denkt", sondern was er gerade
wirklich macht (und wenn er nur nachdenkt, mit etwas Laune).

**Neu: Er kann jedes installierte Programm öffnen.**
Unity, Roblox Studio, Blockbench, Blender, Godot, osu!, OBS, VS Code – oder was
sonst auf dem Rechner installiert ist: Qwirbel findet es selbst (auch über das
Startmenü) und startet es, auf Wunsch gleich mit dem richtigen Projekt oder der
richtigen Datei. Auch Server-Start-Skripte und .jar-Dateien laufen so. Und mit
einem Blick auf den Bildschirm prüft er danach, ob das Fenster wirklich da ist.

**Er stört dich nicht mehr beim Spielen.**
Arbeitet Qwirbel im Hintergrund, während Sie in einem Vollbild-Programm sind –
Spiel, Präsentation, Film –, dann unterlässt er alles, was Sie da herausreißen
würde: Bildschirmfotos vom ganzen Schirm, neue Fenster, Browser-Starts. Er
arbeitet stattdessen an dem weiter, was ohne Bildschirm geht, oder wartet.
Erkannt wird das über den Vollbild-Zustand von Windows selbst, es funktioniert
also mit jedem Spiel und jedem Programm – ohne Liste. Rechenintensive Sachen
wie Builds und Videoumwandlung laufen zusätzlich mit niedriger Priorität, damit
das laufende Spiel flüssig bleibt.

**Sackgassen fallen sofort auf, nicht nach 40 Minuten.**
Fehlt für die gewünschte Zielplattform das passende Unity-Modul, sagt er das in
der ersten Sekunde – samt der Liste, welche Module wirklich installiert sind,
und wo man das nachinstalliert. Vorher wurde stundenlang an etwas gebaut, das
gar nicht gebaut werden kann. Auch ein fehlender Unity-Login im Hintergrund-
Modus wird jetzt als solcher benannt.

**Neu: Er kompiliert wirklich – auch Unity.**
Ein eigenes Bau-Werkzeug erkennt selbst, was für ein Projekt vorliegt (Unity,
Android/Gradle, Maven, npm, .NET, Rust, Go, CMake, Python) und nimmt den
richtigen Befehl, statt ihn zu raten. Bei Unity baut es ohne Editor-Fenster –
die dafür nötige Editor-Methode legt Qwirbel selbst ins Projekt, denn ohne sie
gibt es überhaupt keinen Kommandozeilen-Build. Nach einem Fehlschlag stehen die
relevanten Log-Zeilen im Ergebnis, statt „Exit-Code 1". Fehlt das Bauwerkzeug
selbst, sagt er das klar – und tut nicht so, als sei gebaut worden.

**Neu: Er kann Dateien herunterladen.**
Installer, SDKs, Archive, Modelle – alles per direktem Link. Heruntergeladene
Installer startet Qwirbel grundsätzlich nie von selbst; das bleibt eine
bewusste Entscheidung.

**Neu: Verschieben und Umbenennen.** Für jede Datei und ganze Ordner, ohne je
etwas zu überschreiben.

**Leise im Hintergrund.**
Bisher blitzte bei jedem Befehl ein schwarzes Konsolenfenster auf – bei einem
Bauauftrag mit dutzenden Schritten also dutzende Male. Alle Hintergrund-Prozesse
laufen jetzt unsichtbar.

**Er sieht einzelne Programm-Fenster.**
Statt nur den ganzen Bildschirm kann er sich gezielt ein Fenster ansehen –
Unity, Roblox Studio, den Browser, einen Editor – auch wenn etwas davor liegt.
Ohne Angabe listet er erst alle offenen Fenster auf und sucht sich das richtige.

**Der Browser meldet dich nicht mehr ab.**
Läuft der Browser bereits ohne Fernsteuerungs-Port, wurde bisher ein zweiter
gestartet: der Port kam nie, Fenster sprangen auf, im schlimmsten Fall war man
hinterher ausgeloggt. Jetzt erkennt Qwirbel das und sagt in einem Satz, was zu
tun ist, statt das laufende Fenster durcheinanderzubringen.

**Sagst du ein Modell, nimmt er dieses Modell.**
Stand der Modellname nur im Auftragstext („mach das Video mit LTX"), hat die
Pipeline ihn nie gesehen und ihren Standard genommen. Jetzt wird der Name im
Auftrag erkannt und auf den wirklich vorhandenen Workflow abgebildet.

**Der Schlussbericht ist jetzt eine Tabelle.**
Am Ende steht, was getan wurde – eine Zeile pro Arbeitsschritt mit dem echten
Ergebnis (Pfad, Zahl, Zustand), darunter zwei bis vier Sätze und, falls etwas
offen blieb, eine ehrliche „Offen:"-Zeile.

**Neu: Er kann Bilder und Videos wirklich ansehen.**
Bisher konnte Qwirbel nur auf den Bildschirm schauen – ein Bild auf der
Festplatte musste er im Browser öffnen, und genau daran blieb er hängen (der
Browser ist für Webseiten da, nicht für Screenshot-Ordner). Jetzt sieht er sich
Bilddateien direkt an (Auflösung, Motiv, welcher Text draufsteht) und bei
Videos prüft er Länge, Auflösung, Bildrate und ob überhaupt Ton drauf ist –
plus mehrere Einzelbilder über die ganze Länge verteilt, die er ebenfalls
ansieht. So kann er ein fertiges Video wirklich beurteilen, statt „sieht gut
aus" zu behaupten. Fertige Ergebnisse legt er zum Anschauen in den Chat. Und
wer ihm ein lokales Bild in den Browser schicken will, bekommt jetzt sofort den
richtigen Weg gezeigt, statt anderthalb Minuten auf einen Timeout zu warten.

**Neu: Fertige Pakete hochladen.**
Ein Werkzeug für den Upload fertiger Video-Pakete – wahlweise erst als
Trockenlauf, bei dem garantiert nichts rausgeht. Öffentliches Posten gilt dabei
ausdrücklich als Aktion mit Außenwirkung und läuft durch die
Sicherheitsabfrage.

**Neu: Er baut sich eigene Werkzeuge.**
Wenn er dieselbe Handarbeit zum zweiten Mal macht, kann er sich daraus ein
eigenes Werkzeug mit Namen bauen. Ab dann ruft er es einfach auf – auch in
späteren Aufträgen. Selbstgebaute Werkzeuge laufen durch dieselbe Absicherung
wie ausgeführter Code und können nie ein eingebautes Werkzeug überschreiben.

**Neu: Ergebnisse als ZIP.**
Ein eigenes Pack-Werkzeug schnürt am Ende den Projektordner zusammen. Ein
vorhandenes ZIP wird dabei nie überschrieben.

**Behoben: Er meldet sich wieder im Chat.**
Sobald Qwirbel eine Projektdatei gelesen hatte, galt anschließend jedes
Mitreden und jedes Umplanen als „Handlung nach fremden Inhalten" – im
Schutzmechanismus gegen versteckte Anweisungen. Ergebnis: eine Rückfrage vor
jeder Wortmeldung, in unbeaufsichtigten Läufen war Mitreden sogar ganz
blockiert. Reden und Planen wirken nur in der eigenen Oberfläche und zählen
jetzt richtigerweise nicht mehr als äußere Wirkung. Zusätzlich erinnert er sich
selbst daran, sich zu melden, wenn er mehrere Schritte lang still war.

## v1.12.0 (Er liest nicht mehr im Kreis – und arbeitet endlich durch)

**Der wichtigste Fix: er vergisst nicht mehr, was er gelesen hat.**
Bei langen Aufträgen konnte es passieren, dass derselbe Ordner und dieselben
Dokumente wieder und wieder gelesen wurden, ohne dass je etwas entstand.
Grund war eine zu kleine Gedächtnis-Grenze: sie richtete sich immer nach dem
kleinen lokalen Kontextfenster, selbst wenn ein großes Cloud-Modell arbeitete.
Nach dem dritten Lesevorgang fiel der erste wieder heraus – also las er neu.
Jetzt richtet sich das Gedächtnis nach dem Modell, das wirklich arbeitet: ein
großes Modell behält seine gesamte Lektüre, und es gibt keine künstliche
Obergrenze mehr. Er entscheidet selbst, was er liest.

**Windows-Befehle funktionieren jetzt wirklich.**
Bisher liefen alle Befehle durch eine Unix-Shell – auch echte Windows-Befehle.
Die scheiterten damit reihenweise, und PowerShell-Skripte (`.ps1`) waren gar
nicht startbar. Wer also Aufgaben mit fertigen Windows-Skripten abschließen
wollte, kam nie ans Ziel. Jetzt wählt Qwirbel die passende Umgebung selbst und
sagt bei einem Fehler auch dazu, in welcher er gelaufen ist – so korrigiert er
sich selbst statt dreimal dasselbe zu probieren.

**Neu: der Mühe-Regler – wie viel Sorgfalt soll er sich geben?**
Jeder Arbeitsplatz hat einen eigenen Regler von 1 bis 5, mit passenden
Begriffen: im Chat geht es von „Knapp" bis „Maximal", bei Aufgaben von
„Schnell" bis „Maximal", beim Programmieren von „Schnell" bis „Maximal
sorgfältig". Der Regler ist keine Deko – er steuert, wie viele Arbeitsschritte
erlaubt sind, wie groß ein Plan werden darf, ob zusätzlich nachgedacht wird und
wie oft er selbst nachbessert. Auf der höchsten Stufe bekommt der Knopf eine
kleine Pixel-Animation. Jeder Tab merkt sich seine eigene Stufe.

**Neu: fertige Aufträge auf einen Klick.**
Im Aufgaben- und Programmier-Tab gibt es einen „Aufträge"-Knopf mit
vorbereiteten Aufträgen. Eigene kommen dazu, indem man eine Datei
`PROMPT-meinauftrag.txt` auf den Schreibtisch legt – sie erscheint dann
automatisch in der Liste, passend zum jeweiligen Tab.

**Neu: PE – er sagt dir beim Schreiben, was noch fehlt.**
Ein Knopf „PE" im Eingabefeld. Ist er an, liest ein kleines Modell direkt auf
Ihrer Grafikkarte mit, was Sie tippen, kennt dabei Ihre eigenen Angaben aus dem
Wissensbereich – und nennt die eine Sache, die dem Auftrag noch fehlt. Aus
„erstelle mir ein Minecraft-Plugin" wird so der Hinweis „für Paper 1.21".
Mit der Tab-Taste hängen Sie den Vorschlag an, oder Sie schreiben selbst weiter.
Nichts verlässt dabei den Rechner, und ohne den Knopf passiert gar nichts.

**Sein Gedankengang bleibt jetzt stehen.**
Was Qwirbel während der Arbeit erzählt – und was man ihm dazwischenschreibt –
stand bisher nur im Fenster und war nach jedem Neuladen weg. Bei einem Auftrag
über eine Stunde verlor man damit die ganze Erzählung. Jetzt bleibt sie im
Verlauf und ist auch im Export enthalten.

**Erledigtes bleibt erledigt.**
Wenn Qwirbel seine Aufgabenliste unterwegs anpasste, konnten schon abgehakte
Punkte wieder als offen auftauchen und ein zweites Mal abgearbeitet werden.
Das passiert nicht mehr.

**Ehrliche Abschlussmeldung.**
Die Zusammenfassung am Ende stützt sich jetzt auf eine echte Zählung der
benutzten Werkzeuge. Sie kann nicht mehr behaupten, es hätten keine Werkzeuge
zur Verfügung gestanden, wenn tatsächlich damit gearbeitet wurde.

## v1.11.1 (Plan-Karte übersteht Ablenkung, kein sinnloses Warten mehr)

**Ein geplanter Auftrag verschwindet nicht mehr.**
Wer einen Plan mit vielen Schritten bestätigen wollte, aber währenddessen
kurz das Fenster wechselte, sah die LOSLEGEN-Karte danach nicht mehr – der
Auftrag wirkte, als wäre er nie gestellt worden. Die Karte übersteht jetzt
jeden Fensterwechsel und jedes Nachladen, bis sie beantwortet ist. Im
Work- und Code-Tab wurde außerdem der eigene Auftragstext bisher gar nicht
gespeichert – nach einem Neuladen war er weg, obwohl gearbeitet wurde.
Beides ist jetzt behoben.

**Kein endloses Wiederlesen mehr ohne Ergebnis.**
Bei sehr langen Aufträgen konnte es passieren, dass dieselbe Handvoll
Dateien wieder und wieder gelesen wurde, ohne dass je etwas gebaut wurde –
und am Ende kam eine falsche Entschuldigung ("die Werkzeuge standen nicht
zur Verfügung"), obwohl tatsächlich gearbeitet wurde. Jetzt bekommt der
Assistent eine klare Ansage, sobald er dieselbe Sache dreimal gelesen hat
("das ändert sich nicht – handle jetzt"), und die Abschlussmeldung stützt
sich auf eine echte Zählung der genutzten Werkzeuge, statt sich etwas
auszudenken.

## v1.11.0 (Er vergisst nicht mehr, was er gerade gelesen hat)

**Das Gedächtnis zwischen den Arbeitsschritten.**
Bisher bekam jeder Schritt vom vorherigen nur zwei Zeilen mit. Wer in
Schritt 6 fünf Dokumente liest, stand in Schritt 7 wieder am Anfang – und
las alles noch einmal. Bei langen Aufträgen kam der Assistent so nie zum
Ende. Jetzt trägt er echtes Wissen von Schritt zu Schritt weiter, und die
Budgets richten sich automatisch nach dem Kontextfenster des gewählten
Modells: ein großes Cloud-Modell nutzt viel, ein kleines lokales genau so
viel, dass seine Regeln nicht verdrängt werden.

**Zwei neue Werkzeuge für den Alltag.**
Dateiinfos auf einen Griff – Größe, Datum und bei Video oder Ton auch Länge
und Auflösung, praktisch zum Prüfen fertiger Videos. Und ein Warten, das auf
einen Dienst horchen kann, statt blind Zeit verstreichen zu lassen.

**GLM-5.2 lokal (Colibri) startet jetzt zuverlässig.**
Nach einem Neustart fährt die Engine von selbst wieder hoch, alte Instanzen
werden vorher sauber beendet und der Netzwerk-Port wird abgewartet – vorher
konnten zwei Engines gleichzeitig laufen und sich gegenseitig blockieren.
Außerdem beendet die Antwort jetzt sauber, statt endlos weiterzuschreiben.

*Ehrlicher Hinweis zur Geschwindigkeit:* dieses Modell rechnet auf dem
Prozessor und liefert rund 0,4 Wörter pro Sekunde. Es eignet sich für eine
einzelne, tiefe Frage – nicht für laufende Arbeitsaufträge. Dafür bleibt ein
Cloud-Anbieter oder ein kleineres lokales Modell die bessere Wahl.

**Kleinere Korrekturen.**
Läuft eine Aufgabe, erscheint sie nur noch einmal in der Übersicht (vorher
konnte dasselbe Kästchen doppelt auftauchen). Bestätigte Pläne werden
protokolliert, damit sich ein Startproblem nachvollziehen lässt.

## v1.10.0 (Der Assistent arbeitet wirklich selbstständig)

Diese Version schließt die Lücke zwischen „kann es theoretisch" und „macht es
auch". Der Assistent bekommt Augen, Hände und die Freiheit, sie zu benutzen.

**Er sieht jetzt, was er tut – in einem echten Browser.**
Qwirbel kann Webseiten, Bilder und Videos öffnen, den sichtbaren Text lesen,
bei Bedarf den HTML-Quelltext ansehen, Bildschirmfotos machen, klicken und
tippen. Er benutzt dafür Ihren eigenen Browser – also den, in dem Sie
angemeldet sind. Es werden keine Passwörter gespeichert und keine
Zugangsdaten irgendwohin übertragen.

Rechts in der App gibt es dafür ein **Browser-Fenster**: Adresse eintippen,
öffnen, und Sie sehen dasselbe Bild wie der Assistent. Das Fenster ist immer
erreichbar, auch wenn gerade nichts offen ist.

Findet Qwirbel keinen Browser (Brave, Chrome, Edge, Chromium, Vivaldi, Opera
werden gesucht), nutzt er einen **mitgelieferten** – dann funktionieren
Seiten mit Login allerdings nicht, und die App sagt das auch.

**Mehrere Aufgaben gleichzeitig.**
Work und Code (und weitere Chats) arbeiten parallel, jeder mit eigenem
Anbieter und eigener Aufgabenliste. Rechts steht ein Kästchen pro laufender
Aufgabe. Der Stop-Knopf beendet genau die Aufgabe, bei der Sie stehen – die
andere läuft weiter.

**Er kann nachsehen, statt zu raten.**
Neu: eine Übersicht über ein ganzes Projekt (Ordnerbaum, alle Dokumente, wo
der Quellcode wirklich liegt), eine Statusabfrage für laufende Dienste
(Sprachmodell, Bild-Generierung, Browser, freier Grafikspeicher, vorhandene
Werkzeuge) und eine Prozess-Suche. Für die Bild- und Video-Erzeugung kann er
jetzt selbst prüfen, ob ComfyUI läuft, es bei Bedarf starten, die vorhandenen
Arbeitsabläufe auflisten und gezielt einen davon wählen.

**Die häufigste Blockade ist weg.**
Bisher wurde jeder wiederholte Werkzeug-Aufruf abgewiesen – auch reines
Nachlesen. In langen Aufgaben führte das dazu, dass der Assistent sich selbst
ausbremste und am Ende nichts fertigstellte. Jetzt darf er beliebig oft
nachschlagen; geschützt bleibt nur, was etwas verändert. Wiederholt er
wirklich eine Aktion, bekommt er das frühere Ergebnis zurück statt einer
Fehlermeldung.

**Autonomie-Stufe 4 und 5 arbeiten durch.**
Vorher fragte Qwirbel bei fast jedem Skript, jedem Bau-Befehl und jeder
unbekannten Webseite nach – die Freigabe-Liste kannte nur wenige Befehle. Ab
Stufe 4 laufen normale Arbeitsschritte ohne Rückfrage. Die Schutzgrenzen
bleiben auf jeder Stufe bestehen: Systembereiche, Formatieren, Herunterfahren,
gefährliche Muster und die geschützten Wissens-Ordner sind weiterhin gesperrt,
Administratorrechte und Geheimnis-Dateien verlangen weiterhin Ihre
Bestätigung.

**Er denkt mit und redet mit.**
Während er arbeitet, schreibt er in normalen Sätzen, was er gerade vorhat und
was er herausfindet. Merkt er, dass sein Plan nicht passt, schreibt er ihn
selbst um – erledigte Schritte behalten ihren Haken. Und Sie können ihm
mitten in die Arbeit hineinschreiben: Ihre Nachricht hat Vorrang, er
berücksichtigt sie beim nächsten Schritt.

**Er behält jetzt, was er liest.**
Bisher wurde jedes Werkzeug-Ergebnis auf wenige hundert Zeichen gekürzt,
bevor es in sein Arbeitsgedächtnis ging. Bei fünf Dokumenten mit zusammen
30 Seiten kamen davon zwei Absätze an – der Assistent las dieselben Dateien
darum immer wieder und kam nie zum Ergebnis. Lesende Werkzeuge haben jetzt
ein echtes Budget, ältere Schritte werden bei Bedarf hinten abgeschnitten
statt vorne.

**Neue Werkzeuge für den Alltag.**
Dateiinfos auf einen Griff – Größe, Datum und bei Video oder Ton auch Länge
und Auflösung (praktisch, um fertige Videos zu prüfen). Und ein Warten, das
auf einen Dienst horchen kann, statt blind Zeit verstreichen zu lassen.

**Ruhiger im Hintergrund.**
Startet Qwirbel einen Browser, springt dieser nicht mehr in den Vordergrund
und unterbricht nicht, was Sie gerade tun.

## v1.9.0 (Der Agent redet mit – und Stop stoppt wirklich)

**Der Stop-Knopf hält jetzt wirklich an.**
Bisher brach er nur die Anzeige ab: das Sprachmodell rechnete im Hintergrund
weiter, die Grafikkarte blieb unter Volllast, und ein bezahlter Anbieter
erzeugte weiter Kosten. Jetzt beendet ein Druck auf STOP die laufende Aufgabe,
schließt die Verbindung zum Modell, gibt den Grafikspeicher frei und stoppt
eine laufende Bild-/Video-Generierung – alles in einem Zug. Auch
Hintergrund-Aufgaben (das automatische Mitlernen nach jedem Chat) werden
beendet, damit nicht Sekunden später wieder ein Modell geladen wird.

**Der Agent erzählt, was er tut.**
In den Tabs Work und Code schreibt Qwirbel während der Arbeit in normalen
Sätzen mit, was er gerade vorhat und was er herausfindet – nicht nur
Werkzeug-Namen. Bei Modellen mit sichtbarem Gedankengang (z. B. GLM) wird
dieser zusätzlich im Chat angezeigt.

**Du kannst dazwischenschreiben.**
Läuft eine Aufgabe, startet Senden keinen zweiten Auftrag mehr: deine
Nachricht geht an den laufenden Agenten. Er liest sie vor seinem nächsten
Schritt, sagt kurz, was er jetzt anders macht – und darf daraufhin seine
Aufgabenliste anpassen.

**Die Aufgabenliste ist nicht mehr in Stein gemeißelt.**
Der erste Plan entsteht, bevor der Agent das Projekt gesehen hat. Merkt er,
dass er nicht passt, schreibt er ihn selbst um; erledigte Schritte behalten
dabei ihren Haken.

**Neu: Projekt-Überblick.**
Ein Werkzeug, das ein fremdes Projekt in einem Zug erfasst – Ordnerbaum, alle
Markdown-Dokumente und die Stelle, an der der Quellcode wirklich liegt
(Build-Ordner, Paket-Caches und `node_modules` werden übersprungen). Damit
legt der Agent neue Dateien nicht mehr neben das Projekt statt hinein.

**KI-Anbieter: Auswahl gilt überall.**
Das Modell-Menü oben rechts wirkt jetzt auch in Work und Code – vorher blieb
dort still das lokale Modell aktiv, obwohl oben ein Cloud-Anbieter gewählt
war. Selbst hinzugefügte, OpenAI-kompatible Anbieter können ab sofort
Aufgaben mit Werkzeugen ausführen und nicht nur antworten. Für GLM-Abos ist
die richtige Adresse voreingestellt; „kein Guthaben" wird nicht mehr als
„Rate-Limit" gemeldet.

**Autonomie-Stufe 5 arbeitet durch.**
Auf der höchsten Stufe fragt Qwirbel nicht mehr vor jedem Bau- oder
Systembefehl nach. Die Sicherheitsprüfung läuft weiter und jeder Durchlass
wird protokolliert; in Firmen-Installationen bleibt die Rückfrage bestehen.

**Neu: GLM-5.2 lokal über Colibri.**
Im Model-Store lässt sich die Colibri-Engine einschalten, die ein
744-Milliarden-Modell auf einem normalen PC betreibt – Festplatte, RAM und
Grafikspeicher als eine Speicherkette. Der Store zeigt Download-Fortschritt
und schaltet das Modell danach im Menü frei. Ehrlicher Hinweis in der App:
unter Windows beschleunigt die Engine nur mit NVIDIA/CUDA, auf AMD läuft sie
über den Prozessor – mit viel Arbeitsspeicher nutzbar, aber langsam.

## v1.8.0 (Drei Arbeitsplätze: Chat · Work · Code)

Die größte Änderung an der Bedienung seit Langem – und sie macht genau eine
Sache: Sie trennt **reden** von **arbeiten**.

**Chat ist jetzt wirklich Chat.**
Der Chat-Tab antwortet, erklärt, schlägt nach, generiert Bilder/Videos/Musik
und nutzt Werkzeuge (MCP) – aber er startet keine Arbeitsaufträge mehr
nebenbei. Dafür kennt er ab sofort immer den **Programm-Kontext**: Version,
Variante, aktives Modell und alle Tabs stehen in jeder Antwort zur Verfügung.
Fragen zur eigenen App werden dadurch spürbar präziser.

Erkennt der Chat trotzdem einen Auftrag, führt er ihn nicht aus, sondern
bietet die **Übergabe** an: eine Karte mit einem Klick – „Im Work-Tab
erledigen" oder „Im Code-Tab bauen". Der Auftrag startet dann dort.

**Neu: der Work-Tab.**
Hier arbeitet der Agent autonom mit seinen echten Werkzeugen: Dateien und
Ordner, Recherche, Downloads, Systemabfragen. Ohne Zeitbudget-Frage, ohne
Bestätigungs-Schleifen. Kleinigkeiten (Dateiname, Ordner, Format) entscheidet
er selbst und nennt sie am Ende – zusammen mit dem Ergebnis und den echten
Pfaden. Gefragt wird nur noch bei echten Blockern: Zugangsdaten, eine
Installation, etwas Unumkehrbares.

**Neu: der Code-Tab.**
Programmieren mit Bau- UND Testpflicht. Qwirbel legt den Projektordner an
(Standard: Desktop/<Name>/), schreibt vollständige Dateien – keine
„TODO"-Stummel – und eine kurze README, und **testet danach wirklich**:
Python-Programme werden ausgeführt, Builds laufen über mvn/npm. Ein Fehler
wird gelesen, gefixt und erneut getestet. Erst wenn es läuft, meldet er
fertig. Die Abschlussprüfung akzeptiert im Code-Tab ausdrücklich keinen
ungetesteten Code mehr.

**Kleinigkeiten dazu:**
- Beide neuen Tabs haben eigene Sessions (bis zu 5), eigene Anbieter-/
  Modellwahl, eigene MCP-Auswahl und den Autonomie-Stufen-Chip.
- „Das bauen" aus der Planung geht jetzt in den Code-Tab statt in den Chat.
- Firmen-Variante: Work und Code sind auch für Mitarbeiter-Konten freigegeben;
  alle Konto-Grenzen (Modelle, Limits, Autonomie, Arbeitsbereich, Filter)
  gelten dort unverändert.
- Bestehende Chats bleiben, wo sie sind – der Chat-Verlauf wandert nicht.

**Ehrliche Grenzen:** Wie gut ein Programm am Ende wird, hängt weiterhin vom
gewählten Modell ab; die Bau- und Testregeln erzwingen den Ablauf, nicht die
Qualität des Codes. Und wie immer: die macOS-Pakete sind gebaut und geprüft,
aber nie auf echter Apple-Hardware gestartet.


## v1.7.0 (Härtung & echter Linux-Beweis: 9 Review-Funde gefixt, Testsuiten laufen jetzt auch beim Kunden)

Eine reine Qualitäts-Version: Ein unabhängiger Review-Durchlauf über die
v1.6.0-Neuerungen (27 Prüf-Agenten, jeder Fund doppelt am echten Code
verifiziert) plus ein kompletter End-to-End-Test des Linux-Pakets auf echtem
Ubuntu 24.04. Alles Gefundene ist gefixt und nachgetestet.

**Sicherheit:**
- **Update-Neustart (Linux/macOS) gehärtet:** Installations-Pfade werden dem
  Neustart-Helfer jetzt als Argumente übergeben statt ins Skript geschrieben –
  ein Ordnername mit Sonderzeichen ($, Backtick, Anführungszeichen) konnte
  vorher den Neustart brechen oder als Shell-Code laufen. Auf echtem Ubuntu
  mit feindseligem Pfad bewiesen.
- **MCP-Sicherheits-Whitelist dicht:** Eine Datei, die nur npx/uvx HIESS
  (z. B. npx.bat mit Pfad), konnte die Whitelist passieren und wurde
  ausgeführt. Jetzt entscheidet der normalisierte Programmname, npx/uvx
  werden IMMER auf die echten Programme aufgelöst, und node läuft nie über
  Batch-Wrapper.
- **API-Schlüssel-Scopes auch im Privacy-Center:** Ein Maschinen-Schlüssel
  mit nur Lese-Scope konnte auf dem Server Papierkorb/Temp leeren und die
  Konten-Übersicht lesen. Alle Privacy-Aktionen verlangen jetzt den
  admin-Scope – wie überall sonst.

**Robustheit:**
- **Mikrofon-Doppelbelegung behoben:** Diktat-Klick bei laufendem
  „Hey Qwirbel"-Lauscher (und umgekehrt) konnte die komplette Audio-Schicht
  töten (dokumentierter PortAudio-Absturz). Beide Seiten teilen sich jetzt
  eine gemeinsame Mikrofon-Reservierung mit klarer Meldung.
- **Konten-Übersicht verliert keine Daten mehr:** Gleichzeitige Änderungen
  (zwei Tabs, Doppelklick) und eine beschädigte Datei konnten still den
  ganzen Bestand überschreiben. Jetzt: Sperre, atomares Schreiben, und eine
  kaputte Datei wird NIE überschrieben, sondern ehrlich gemeldet.
- **KI-Kennzeichnung erhält alle Spuren:** Beim Kennzeichnen von Videos
  gingen Untertitel- und Zweit-Audio-Spuren verloren – jetzt bleiben alle
  Streams und Kapitel erhalten.
- **Kein Doppel-Start nach Update:** Zweimal schnell auf „Neu starten"
  geklickt ergab zwei Instanzen. Der zweite Klick meldet jetzt ehrlich
  „läuft bereits".
- **Sprach-Engine-Wahl abgesichert:** Eine erzwungene, aber nicht
  installierte Engine meldete „verfügbar" und scheiterte dann bei jedem
  Diktat – jetzt fällt Qwirbel automatisch auf die installierte Engine
  zurück. Außerdem blockiert das Vorladen des Sprachmodells nicht mehr den
  ersten Mikrofon-Klick.

**Für Kunden-Installationen:**
- **Die mitgelieferten Testsuiten laufen jetzt auch in gekauften Kopien:**
  Vor der Aktivierung brechen sie mit einer klaren Meldung ab (statt mit
  kryptischen Fehlern), nach der Aktivierung nutzen sie die Geräte-Lizenz
  und laufen normal. Prüfungen, die Herausgeber-Werkzeuge brauchen
  (Lizenz-Server, Release-Packer, Offline-Kit), werden ehrlich
  übersprungen – auf echtem Ubuntu verifiziert (29/29 grün in der
  Verkaufskopie).
- **Linux-Paket end-to-end auf echtem Ubuntu 24.04 bewiesen:** Silent-Setup,
  Backend-Start, Lizenz-Gate, Auto-Neustart – alles live getestet (WSL2).
  macOS bleibt ehrlich ungetestet (kein Mac vorhanden).

## v1.6.0 (Alltag & alle Betriebssysteme: Ein-Klick-Update, schlanke Spracherkennung, Privacy komplett)

Diese Version macht die private Version rund und zieht die neuen Funktionen
sauber über ALLE drei Betriebssysteme (Windows, Linux, macOS) – gleiche
Funktionen, gleicher Update-Weg, egal wo Qwirbel läuft.

**Updates:**
- **Ein-Klick-Update auf jedem System:** Nach „Update anwenden" startet
  Qwirbel sich jetzt überall selbst neu – Windows über einen unsichtbaren
  Neustart-Helfer, Linux mit systemd wie bisher, Linux ohne systemd und
  macOS über einen kleinen Shell-Helfer. Kein „bitte manuell neu starten"
  mehr; das Fenster schließt kurz und kommt mit der neuen Version wieder.

**Spracherkennung:**
- **Neue, schlanke Sprach-Engine (faster-whisper):** Diktieren braucht kein
  torch mehr – rund 1 GB weniger Arbeitsspeicher, deutlich kleinerer
  Download, und die Grafikkarte bleibt komplett für KI-Modelle und
  Bild-Generierung frei. Das Setup installiert automatisch die neue Engine;
  bestehende Installationen mit der alten Engine laufen unverändert weiter
  (umschaltbar über die Einstellung `stt.engine`).

**Privacy-Center – jetzt komplett (9 Bereiche):**
- **Konten-Übersicht:** Alle deine Online-Konten im Blick – welche haben
  kein 2FA, welche waren in einem Daten-Leak, welche nutzt du nie mehr.
  Qwirbel sortiert nach Dringlichkeit und priorisiert auf Wunsch per KI.
  Bewusst KEIN Passwort-Manager: Passwörter werden NIE gespeichert.
- **Privacy-Coach:** Begleitet dich langfristig – merkt sich, was du schon
  umgesetzt hast (Fortschritts-Liste: Empfohlen → In Arbeit → Erledigt) und
  schlägt die nächsten Schritte vor, die darauf aufbauen. Keine generischen
  Tipps.
- **Datei-Hygiene:** Findet doppelte Dateien, große lange nicht angefasste
  Brocken, leere Ordner, alte Downloads und vergessene Screenshots – mit
  Aufräum-Potenzial in GB. Es wird NICHTS gelöscht, nur gefunden.

**MCP-Werkzeuge:**
- **Node.js-Server (npx) laufen jetzt zuverlässig auf allen Systemen:**
  Qwirbel findet npx auch dann, wenn es (noch) nicht im PATH steht –
  Windows-Standardordner, macOS-Homebrew (Intel + Apple Silicon) und
  /usr/local auf Linux. Damit sind Browser-Steuerung (Playwright),
  Gedächtnis-Graph, Dateisystem u. a. aus dem MCP-Shop nutzbar.

**Ehrliche Grenzen dieser Version:** Der neue Auto-Neustart wurde auf
Windows vollständig end-to-end getestet; die Linux/macOS-Variante ist
logisch identisch und shell-getestet, lief aber noch nicht auf echter
Fremd-Hardware. macOS-Pakete sind weiterhin nie auf einem echten Mac
gestartet worden.

## v1.5.0 (Firmen-Server: komplette IT-Roadmap P0 + P1 — 24 Punkte, 1035 automatische Checks)

Der dritte und vierte große Schritt der IT-Roadmap: ALLE verbleibenden
P0-Blocker und ALLE 21 P1-Erwartungen einer IT-Abteilung sind gebaut,
wegwerf-getestet (22 Testsuiten, 1035 Checks grün) und im Administrator-
Handbuch dokumentiert. Alles ist in beiden Paket-Linien enthalten – die
Firmen-Funktionen sind in der Normal-Variante schlicht abgeschaltet;
Schutz-Features (KI-Kennzeichnung, Injektions-Gate, Sandbox) wirken überall.

**Identität & Zugang:**
- **Single Sign-On (OIDC):** Entra ID, Keycloak, Google Workspace, Okta –
  Authorization-Code-Flow mit echter Signatur-Prüfung, Auto-Provisioning,
  Gruppen→Rollen-Mapping. Login-Button erscheint nur bei aktiviertem SSO.
- **LDAP / Active Directory:** Login gegen AD/OpenLDAP (Service-Bind oder
  direkter User-Bind), Rollen aus Verzeichnis-Gruppen, TLS empfohlen.
- **Gruppen und Richtlinien:** Richtlinien (Modelle, Limits, Autonomie,
  Filter, MCP) an Gruppen hängen statt an 200 Einzelkonten; Vererbung
  Konto > Gruppe > Standard, wirksam-Anzeige mit Herkunft je Feld.
- **Mehr Rollen:** Auditor (Protokoll lesen, nichts ändern), Team-Leitung
  (nur eigene Abteilung verwalten), Nur-Lesen – serverseitig durchgesetzt,
  Rollenwechsel widerruft Sitzungen sofort.
- **Zwei-Faktor (TOTP) + Passwort-Richtlinien:** Authenticator-App-TOTP
  (RFC 6238), Backup-Codes, Pflicht für Admins konfigurierbar, Mindestlänge,
  Sperrliste, Erst-Passwort muss geändert werden.

**Betrieb:**
- **Docker-Image + docker-compose** (Volumes, Healthchecks, GPU-Wege
  dokumentiert) und **Kubernetes-Helm-Chart** (PVC, Probes, gehärteter
  Sicherheitskontext).
- **Überwachung:** /metrics im Prometheus-Format + fertiges Grafana-
  Dashboard; strukturierte JSON-Logs nach Datei/stdout/syslog (RFC 5424);
  SIEM-Versand in CEF/LEEF nur für Sicherheits-Ereignisse.
- **Unbeaufsichtigte Installation** (`setup.py --still --antworten datei.json`,
  maschinenlesbare Exit-Codes für Intune/JAMF/SCCM) und **Air-Gapped-
  Installation**: Offline-Wheel-Paket + Offline-Lizenzaktivierung per
  signierter Datei – ganz ohne Internet.
- **Updates gestaffelt, mit Rückweg:** Kanäle stabil/test/LTS,
  deterministischer Rollout-Prozentsatz, Versions-Pin, Wartungsfenster,
  Rollback holt auch die Daten zurück.

**Sicherheit:**
- **Verschlüsselung ruhender Daten** (optional): AES-256-GCM für Chats,
  Wissen und Anhänge; Schlüssel per DPAPI (Windows), Datei oder externem
  Schlüssel-Kommando (KMS-Anbindung); schonende Migration im laufenden
  Bestand.
- **Abfluss-Kontrolle (DLP):** IBAN (echte Prüfziffer), Kreditkarten,
  API-Keys, Private Keys und eigene Muster werden blockiert, maskiert oder
  gemeldet, BEVOR etwas zu einem externen KI-Anbieter geht.
- **Schutz gegen Prompt-Injection:** Fremd-Inhalte (Web/Mail/Dateien) werden
  als gerahmte DATEN behandelt; externe Wirkungen (Shell, Netz, Uploads)
  brauchen danach IMMER eine Rückfrage – auch bei voller Autonomie.
- **Code-Ausführung eingesperrt:** Windows-Job-Objekte mit echtem
  Speicher-Limit und Prozessbaum-Kill, Zeit-Limits, Jail-Verzeichnis,
  bereinigte Umgebungsvariablen; Docker-Backend mit --network none als
  harte Grenze.
- **Abhängigkeiten-Überwachung:** täglicher OSV.dev-Abgleich der
  installierten Pakete mit Alarm bei kritischen Lücken, security.txt
  (RFC 9116) und SECURITY.md mit zugesagten Reaktionszeiten.

**Verwaltung:**
- **Admin-API, CLI und Maschinen-Schlüssel:** qw_sk_-Schlüssel mit Scopes
  (lesen/chat/admin), Rotation, Rate-Limits; `scripts/qwirbel_admin.py`
  für Ein-/Austritte ohne Klicken (sperren + Sitzungen beenden + Daten
  exportieren/löschen als EIN Vorgang).
- **Token-Budgets:** echte Token-Messung (Ollama/Anthropic/OpenAI-Metadaten),
  Tages-Budgets mit Gruppen-Vererbung, Warnschwellen, Auswertung pro
  Abteilung, Prometheus-Serie.

**Wissen (meistgewünscht):**
- **Firmenwissen durchsuchbar (RAG):** Wissensquellen (Ordner, txt/md/html/
  PDF), hybride Suche (Vektor + Schlüsselwort, Embeddings über Ollama),
  Antworten mit Quellenangabe, `/wissen`-Befehl im Chat.
- **Rechte-treue Suche:** Berechtigungen der Quelle wandern mit – gefiltert
  wird VOR dem Scoring; die Gehaltsliste bleibt selbst bei Prompt-Tricks
  unsichtbar (in 8 automatischen Checks bewiesen).

**EU-KI-Verordnung (Art. 50):** KI-Transparenz-Hinweis in der App, „KI-
generiert"-Kennzeichnung in der Oberfläche und maschinenlesbare Metadaten
in erzeugten PNG/MP4/Audio-Dateien; Einordnung + Betreiber-Checkliste in
`docs/EU-KI-VO.md`.

Ehrliche Grenzen stehen im Administrator-Handbuch: SSO/LDAP gegen Mock-
Verzeichnisse getestet (noch nicht gegen echtes Entra ID/AD), Docker-Build
und Helm-Rendering auf echten Hosts ausstehend, MP4-/Audio-Kennzeichnung
braucht ffmpeg, C2PA-Signatur folgt separat.

## v1.4.0 (Firmen-Server: Nachweise, Sicherung, DSGVO, Mandantentrennung bewiesen)

Der zweite große Schritt der IT-Roadmap – die Punkte, mit denen eine
IT-Abteilung den Betrieb abnimmt:

- **Audit-Log fälschungssicher:** Jede Protokollzeile ist per Hash-Kette mit
  ihrer Vorzeile verkettet – nachträglich geänderte oder gelöschte Zeilen
  fallen bei der Prüfung auf (Admin-Tab → Audit → „Kette prüfen"). Dazu
  automatische Rotation großer Logs, eine einstellbare Aufbewahrungsfrist
  und ein Export für Revision/Datenschutzbeauftragte (JSONL, filterbar).
- **DSGVO-Paket je Konto:** Auskunft (was ist gespeichert), Export als ZIP
  und Löschung (wahlweise endgültig) – auf Knopfdruck im Admin-Tab.
  Mitarbeiter können ihre eigenen Daten selbst exportieren.
- **Mandantentrennung bewiesen, nicht behauptet:** Eine automatische
  Testsuite (57 Einzel-Checks, `tests/test_mandanten_trennung.py`) belegt,
  dass kein Konto an Daten eines anderen kommt – inklusive Pfad-Tricks und
  geteilter Ordner. Dabei gefundene Lücken wurden geschlossen: Generierungs-
  Ausgaben, Chat-Zusammenfassungen, Verlaufssuche, Chat-Export, Anhänge,
  Kalender/Aufgaben (jetzt je Konto getrennt), Tagebuch/Mail/Uploads des
  Betreibers und die Einstellungs-Ansicht sind für Mitarbeiter-Konten
  sauber getrennt bzw. gesperrt.
- **Voll-Sicherung mit getestetem Rückweg:** Konten, alle Chats, Wissen,
  Arbeitsbereiche, Lizenz, Workflows und Audit-Log in einem ZIP
  (Admin-Tab → Betrieb oder `scripts/backup_restore.py`). Der Restore ist
  automatisiert durchgespielt und legt vorher selbst eine Sicherung an.
- **Konfiguration per Umgebungsvariablen:** Jede Einstellung ist jetzt auch
  ohne UI setzbar (`QWIRBEL_CFG_SERVER__PORT=11100` …) – für Ansible,
  Docker und automatisiertes Ausrollen.
- **Administrator-Handbuch** (`docs/ADMIN-HANDBUCH.md`): Installation,
  Härtung, Sicherung, Update/Rollback, Fehlersuche, Kapazität.
- **Neu für die IT:** Nutzer-Import aus CSV, Wartungsmeldung als Banner für
  alle (auch am Login), Diagnose-Paket ohne Geheimnisse für Supportfälle,
  Selbstbedienung für Mitarbeiter (Passwort ändern, überall abmelden).
- **Härtungen & Fixes:** HTTPS wirkt jetzt auch beim Start über die
  Programm-Starter (nicht nur den Dienst); `/lizenz/status` gibt den
  Lizenzschlüssel nicht mehr unauthentifiziert preis; der Chat-Export
  exportiert wieder Inhalte statt leerer Nachrichten; Linux-Handstart
  startet ComfyUI nicht mehr doppelt; Setups prüfen die Python-Version
  ehrlich (3.10+); README-Angaben (Update-Weg, TLS-Befehl, systemd) auf den
  echten Stand gebracht.

## v1.3.1 (Universelle Pfade, Datei-Vorlesen, Gemini 3.6)

- **Aufgaben landen jetzt IMMER am richtigen Ort.** Lokale Modelle erfanden
  gern Linux-Pfade wie `/home/…/Schreibtisch` – auf Windows entstand daraus
  ein unsichtbarer Phantom-Ordner `C:\home\…`, und „erstelle auf meinem
  Desktop" wirkte wie ein Placebo. Neu: Jeder vom Modell genannte Pfad wird
  vor der Ausführung auf das ECHTE System übersetzt (Home, Desktop,
  Downloads – Windows/Linux/macOS). Zusätzlich lernen die Skills dem Modell
  keine fremden Pfade mehr: Beispiele nutzen Platzhalter, die beim Laden mit
  den echten Pfaden des jeweiligen PCs gefüllt werden.
- **„Lies die Datei auf meinem Desktop" funktioniert jetzt zuverlässig** –
  mit jedem Modell: Qwirbel findet die Datei (auch bei ungefährem Namen),
  zeigt sie als Chip und listet den Inhalt direkt im Chat. Binärdateien
  werden ehrlich gemeldet (Bilder als Vorschau).
- **Gemini 3.6 Flash + 3.5 Flash (-Lite)** sind im Modell-Menü wählbar
  (Googles aktuelle Modelle, GA seit 21.07.2026); bestehende Konfigurationen
  bekommen die neuen Modelle automatisch dazu. Gemini-Antworten sind sauber:
  interne „Denk"-Abschnitte der 3er-Modelle landen nicht mehr im Chat, und
  Werkzeug-/Agent-Züge werden per JSON-Zwang angefragt – Tool-Calls und MCP
  über die Google-API laufen damit deutlich stabiler.
- **„Was weißt du über mich" antwortet wieder ehrlich** aus dem eigenen
  Wissen (statt „ich habe keinen Zugriff auf persönliche Informationen") –
  die Regel steht jetzt zusätzlich am wirksamen Ende des System-Prompts.

## v1.3.0 (Firmen-Server: Anmeldung, Verschlüsselung, Betrieb)

Der erste Schritt der IT-Roadmap. Es geht nicht um neue Funktionen, sondern um
die Punkte, an denen eine IT-Abteilung bisher „nein" gesagt hat.

- **Anmeldung mit Benutzername und Passwort.** Auf dem Firmen-Server fragt der
  Login jetzt nach einer Kennung. Vorher genügte das Passwort allein – das
  Konto wurde darüber *gesucht*, und **zwei Mitarbeiter mit demselben Passwort
  landeten im selben Konto** (es gewann der erste Treffer). Der bequeme Weg
  bleibt über `server.nur_passwort_login` einschaltbar, ist in neuen
  Firmen-Paketen aber ab Werk aus. Die private Version ist unverändert.
- **Anmeldungen lassen sich widerrufen.** Die Sitzungs-Token sind signiert und
  galten bisher bis zum Ablauf weiter – auch nach einer Kündigung oder wenn ein
  Handy verloren ging. Jetzt trägt jeder Token eine Epoche; wird sie erhöht,
  sind alle vorher ausgegebenen Anmeldungen sofort wertlos. Das passiert
  **automatisch**, sobald ein Konto gesperrt, gelöscht oder mit einem neuen
  Passwort versehen wird. Neuer Endpunkt `POST /auth/sessions/revoke`: jeder
  kann sich selbst überall abmelden, die IT jeden anderen – und im Notfall alle
  auf einmal. Bestehende Anmeldungen überstehen das Update.
- **HTTPS.** Bisher lief alles unverschlüsselt; Login-Passwort und Firmenwissen
  gingen im Klartext durchs Netz. Neu: `python backend/tls_setup.py` erzeugt ein
  Zertifikat und schaltet TLS ein. Eigene Zertifikate (Firmen-CA, Let's Encrypt)
  können einfach in denselben Pfaden liegen. Ohne Konfiguration bleibt alles
  wie bisher bei HTTP.
- **Schutzheader** für jede Antwort (`X-Content-Type-Options`, `X-Frame-Options`,
  `Referrer-Policy`), HSTS nur bei aktivem TLS – über HTTP wäre es wirkungslos
  und bei einer Fehlkonfiguration monatelang blockierend.
- **Betriebs-Endpunkte für Rechenzentren:** `/healthz` antwortet ohne jede
  Abhängigkeit (Liveness), `/readyz` prüft Ollama und Lizenz und meldet **503**,
  wenn der Knoten nicht bereit ist – damit ein Loadbalancer ihn aus der Rotation
  nimmt, statt Nutzer in einen kaputten Dienst zu schicken.
- **Gültigkeitsdauer der Anmeldung einstellbar** (`server.token_tage`). 90 Tage
  sind für ein privates Handy bequem, für einen Büro-Arbeitsplatz zu lang.
- **Stückliste (SBOM) im CycloneDX-Format** liegt jedem Paket bei, dazu eine
  **SHA256-Prüfsummenliste** neben den ZIPs. Beides fragt der Einkauf inzwischen
  ab; es zu liefern kostet fast nichts.
- **Packer härter:** Schlüssel und Zertifikate (`*.key`, `*.crt`, `*.pem`, …)
  sowie `config/tls/` können nicht mehr versehentlich in ein Paket geraten –
  sonst läge der private Schlüssel des Entwicklungsrechners in jeder
  verkauften Kopie.

## v1.2.0 (Installation repariert – Windows, Linux und macOS)

Diese Version bringt keine neuen Funktionen, sondern räumt die Installation
auf. Nutzer meldeten zwei Dinge: **„uvicorn fehlt"** und **„start.bat macht
einfach nichts"**. Beides hatte dieselbe Wurzel.

- **Setup und Start benutzen jetzt garantiert denselben Python.** Bisher
  installierte `setup.py` in den Python, mit dem es gestartet wurde (meist
  `py -3`), die Starter suchten aber ein `.venv` – das nie angelegt wurde.
  Sie fielen deshalb auf irgendein `python` aus dem PATH zurück, und das war
  oft eine **zweite Python-Installation ohne die Pakete** → genau der Fehler
  `ModuleNotFoundError: uvicorn`. **Neu:** `setup.py` legt auf allen drei
  Systemen ein `.venv` im Qwirbel-Ordner an und installiert dort hinein; die
  Starter nehmen ausschließlich dieses `.venv`.
- **„start.bat macht nichts" behoben.** Zwei Ursachen:
  1. Windows legt unter `WindowsApps` Platzhalter namens `python.exe` /
     `pythonw.exe` ab, die nur den Store öffnen. Die alten Skripte prüften mit
     `where` – das **findet** den Platzhalter, startet aber nichts. Jetzt wird
     jeder Kandidat wirklich **gestartet und geprüft**, bevor er benutzt wird.
  2. Ein Batch-Fehler (`%errorlevel%` innerhalb eines Klammer-Blocks wird zu
     früh ausgewertet): `start.bat` hielt selbst dann einen Python für
     gefunden, wenn gar keiner da war – und lief ins Leere, ohne die
     vorgesehene Fehlermeldung zu zeigen.
- **`start_qwirbel.bat` scheitert nicht mehr stumm.** `pythonw.exe` hat keine
  Konsole – ging etwas schief, sah der Nutzer buchstäblich nichts. Jetzt wird
  vorher **mit** Konsole geprüft, ob Qwirbels Kern lädt; sonst kommt eine
  klare Meldung samt Original-Fehlertext.
- **Qwirbel meldet sich jetzt, wenn der Start scheitert.** Kam das Backend
  nicht hoch, öffnete `app.pyw` einfach kein Fenster und blieb still im Tray
  hängen – ohne Konsole sah der Nutzer buchstäblich nichts. Jetzt kommt ein
  Fenster mit dem Grund (unter Windows/macOS/Linux jeweils systemeigen).
  Häufigster Grund, der jetzt im Klartext dasteht: **„Port 11000 ist schon
  belegt"** – meist läuft Qwirbel bereits im Tray.
- **Die Setup-Prüfung prüft jetzt das Richtige.** Sie testete die Module im
  Setup-Interpreter und meldete ✅, während der Start-Interpreter sie gar nicht
  hatte. Jetzt wird im `.venv` geprüft – also genau dort, wo Qwirbel startet.
- **Neu für Linux/macOS: `setup.sh` und `start.sh` im Hauptordner.** Ein Weg,
  der auf beiden Systemen gleich heißt und ohne sudo auskommt. Die großen
  Skripte (`linux/ubuntu_setup.sh`, `mac/mac_setup.sh`) bleiben für das volle
  System-Setup.
- **macOS: Doppelklick auf `mac/start_qwirbel.command` funktioniert wieder.**
  Die Release-ZIPs wurden ohne Unix-Rechte gepackt – nach dem Entpacken war
  keine Datei ausführbar, der Finder öffnete das Startskript im Editor. Die
  ZIPs tragen die Rechte jetzt; zusätzlich setzen `setup.py` und die Setup-
  Skripte sie beim Einrichten nachträglich.
- **Kein stiller Rückfall mehr auf System-Python** in `linux/start.sh` und
  `mac/start_qwirbel.command`. Auf Ubuntu ist systemweites `pip` ohnehin
  gesperrt (PEP 668) – dort lagen die Pakete nie. Statt eines kryptischen
  Import-Fehlers kommt jetzt der Hinweis, das Setup auszuführen.
- **`setup.bat` verschluckt keine Fehler mehr:** Bricht das Setup ab, sagt es
  das und endet mit Fehlercode, statt „fertig" zu suggerieren.
- **Robustere Installation:** pip wird im `.venv` aktualisiert, und ein
  fehlgeschlagener Durchlauf wird einmal ohne pip-Cache wiederholt (ein halb
  geladenes Wheel im Cache war eine häufige Fehlerquelle).

## v1.1.9 (Auto-Switch der KI-Anbieter & Hyperspace-Cluster)
- **Auto-Switch / Failover (neuer Tab „KI-APIs"):** Alle KI-Anbieter (Claude,
  Gemini, GLM, Grok, OpenAI, Mistral, Groq, eigene …) stehen wie Ollama direkt
  im Chat als Buttons bereit. Neu: **Auto-Switch** – bricht ein Anbieter ab
  (Rate-Limit 429, Server-Fehler, Timeout, leere Antwort), macht der **nächste
  der Kette nahtlos weiter**. Laufende Aufgaben/Code werden nicht unterbrochen.
  Das lokale Ollama bleibt immer als letztes Netz (kann nie Rate-Limit). Die
  Reihenfolge der Kette ist frei einstellbar; ein Schalter direkt im Chat-Menü
  aktiviert Auto-Switch. Wirkt in Chat, Aufgaben, Planung und MCP. Vorbild:
  LiteLLM/Bifrost.
- **Hyperspace – PC-Cluster im Netz (neuer Tab):** Mehrere Qwirbel-PCs im
  gleichen Netz zu einem Verbund zusammenschließen. Jede Maschine meldet live
  ihren Status (GPU/VRAM, Warteschlange, CPU, Modelle); Aufgaben gehen an die
  **freieste Node** („Blockaufteilung"). PCs per Adresse verbinden oder das Netz
  automatisch durchsuchen. Beitritt nur mit gemeinsamem **Cluster-Schlüssel**
  (Sicherheit). Für Modelle, die größer als eine GPU sind, bindet die
  **exo-Bridge** eine exo-Cluster (echtes Modell-Sharding über mehrere Geräte)
  wie einen normalen KI-Anbieter ein. Vorbild: exo (ring memory weighted
  partitioning).

## v1.1.8 (Chat-Sync, Gedankengang im Chat & neues Privacy-Center)
- **Chat-Sync PC ⇄ Handy:** Schreibt ein Gerät etwas, erscheint es **sofort auf
  dem anderen** – kein Neustart, kein F5 mehr. Technisch: das Backend meldet
  jede gespeicherte Nachricht über die Live-Verbindung, das jeweils andere Gerät
  lädt den Verlauf nach (das sendende Gerät ignoriert seine eigene Meldung, damit
  laufende Antworten nicht überschrieben werden). Zusätzlich wird beim
  Wieder-Sichtbarwerden (Handy entsperrt / App aus dem Hintergrund / Tab-Wechsel)
  einmal frisch geladen – das fängt auch ab, wenn die Verbindung zwischendurch
  weg war. **Leeren und „Qwirbeln" synchronisieren ebenfalls.**

- **Gedankengang im Chat:** Ist der **Denken**-Schalter (Modell-Menü) an, siehst
  du bei Denkmodellen (qwen3, qwq …) jetzt live einen aufklappbaren
  **„Gedankengang"**-Block – du liest mit, was Qwirbel überlegt, BEVOR er
  antwortet. Klappt beim Antwort-Start automatisch ein (Antwort im Fokus),
  bleibt aber aufklappbar. Modelle ohne echten Denk-Modus antworten wie bisher.
- **Privacy-Center komplett neu:** Jeder Reiter ist jetzt eigenständig,
  übersichtlich – und die Knöpfe TUN wirklich etwas:
  - **Müll-Scanner:** Caches/alte Downloads/Riesen-Dateien als Liste mit
    **Ordner öffnen** & **Pfad kopieren**; **Temp prüfen → aufräumen** und
    **Papierkorb leeren** (nur nach Bestätigung).
  - **Netzwerk-Monitor:** echte Tabelle (Programm · Verbindung · Ampel) mit
    Kacheln (Gesamt/Aktiv/Lauscht/Verdächtig) und Filter – kein Text-Wust mehr.
  - **Autostart:** Einträge einzeln **deaktivieren/aktivieren** (umkehrbar,
    ohne Admin für Benutzer-Einträge; Windows Registry + Linux XDG).
  - **Updates & App-Leichen:** saubere Programm-Listen (Windows winget / Linux
    apt) mit Versions-Sprung, Filter und – bei Updates – **1-Klick-Aktualisieren**.
  - **Leak-Scanner:** HaveIBeenPwned mit eigenem API-Key (bleibt lokal),
    Ergebnisse als klare Leck-Karten statt JSON. Nur die Adresse geht raus.
  - **KI-Einschätzung** überall optional dazuschaltbar. Nichts verlässt den PC
    (Ausnahme: der Leak-Scan schickt nur die E-Mail-Adresse an HaveIBeenPwned).

## v1.1.7 (Denk-Modus, stabiler Agent, MCP auf Windows, CPU-Modus)
- **Denken-Knopf unten im Chat** (auch in der App): Aufgaben-Denkmodus AN =
  ein Denker-Modell plant jede Aufgabe und prüft am Ende das Ergebnis, das
  Agent-Modell führt aus (Kombi-Modus, `ollama.think_model`). Der Knopf zeigt
  ehrlich an, ob die Modelle installiert sind – fehlt eins, läuft die Aufgabe
  trotzdem (Fallback), mit Hinweis zum Nachladen im Store.
- **Agent deutlich stabiler:** großes Kontextfenster für Agent-Aufgaben
  (vergisst nicht mehr mitten in der Aufgabe seine Schritte), Schutz gegen
  sinnloses Wiederholen und gegen das Überschreiben guter Dateien mit
  kürzerem Inhalt, längere Antworten möglich (große Dateien in einem Zug).
- **Neues Werkzeug `python_ausfuehren`:** der Agent kann Python-Code direkt
  ausführen (rechnen, Daten umformen, Code testen) – ab Autonomie-Stufe 4.
- **MCP läuft jetzt überall out-of-the-box:** `uv`/`uvx` liegt den
  Abhängigkeiten bei (vorher fehlte es auf Windows → kein MCP-Server startete).
  Aufgaben nutzen die aktivierten MCP-Server automatisch (Web-Fetch, Zeit,
  Git, …); im normalen Chat bleibt es wie gehabt zuschaltbar.
- **Model-Store erweitert:** große Modelle für viel RAM (llama3.3:70b,
  llama4:scout, gpt-oss:120b …), qwen3-coder:30b (der Agent-Coder) und das
  Qwen-Agent-Weltmodell – mit ehrlichen RAM-Hinweisen.
- **Settings → ComfyUI/VRAM: Ollama CPU-Modus.** Riesen-Modelle (70B+)
  komplett im Arbeitsspeicher rechnen lassen, wenn sie nicht in den VRAM
  passen. Ein Klick zurück auf Auto (GPU).
- **Windows-Politur:** „ComfyUI neu starten", „Im Browser öffnen" und
  „MCP-Ordner öffnen" funktionieren jetzt auch auf Windows (vorher
  Linux-only). Der ComfyUI-Neustart lehnt ab, solange eine Generierung
  läuft. Linux-Reparatur-Knöpfe melden sich auf Windows ehrlich ab.
- **NEU: Models-Tab → „ComfyUI-Basis".** Alle Modelle, die die mitgelieferten
  Workflows brauchen – **Bild** (z-image-turbo), **Video** (WAN 2.2 + WAN 2.1)
  und **Musik** (ACE-Step 1.5: Musik-Modell, beide Text-Encoder, Audio-VAE) –
  als **1-Klick-Download von Hugging Face** direkt in den richtigen
  ComfyUI-Ordner: Fortschritt, Da/Fehlt-Status je Datei, Gruppen-Übersicht.
  Kein Terminal, kein Modell-Suchen: nach dem Setup die Gruppen laden und
  generieren. Der Setup-Wizard verweist im ComfyUI-Schritt darauf.
- **Workflow-Öffnen öffnet jetzt den RICHTIGEN Workflow.** Vorher zeigte
  ComfyUI beim Öffnen immer den zuletzt offenen Workflow (z. B. Musik) –
  jetzt installiert Qwirbel automatisch einen kleinen Workflow-Öffner in
  ComfyUI: der ÖFFNEN-Knopf lädt exakt den gewählten Workflow im Browser
  und legt ihn zusätzlich in ComfyUIs Workflow-Leiste. Funktioniert auf
  Windows und Linux (einmalig ist ein ComfyUI-Neustart nötig).

## v1.1.6 (Sauberer Gesang, neues Icon, Modell-Liste)
- **Silben-Gesang:** Beim Musik-Generieren werden die Lyrics automatisch in Silben
  zerlegt, damit die KI die Wörter **sauberer singt** ([Verse]/[Chorus]-Marken und
  Zeilen bleiben). Direkt in der Musik-Box an-/ausschaltbar.
- **Länge direkt in der Musik-Box:** Song-Länge (5–240 s) oben per Regler einstellen.
- **Neues App-Icon** (das Qwirbel-Maskottchen) — im Fenster, in der Taskleiste, im
  Browser-Tab und auf dem Desktop.
- **Modell-Download-Liste** (`MODELLE.md`): welche ComfyUI-Modelle (GGUFs & Co.) man
  für Bild/Video/Musik/Bearbeitung braucht und wohin sie gehören.

## v1.1.5 (Stimmen, Cover, Preset-Menü)
- **Stimmen im Chat** (Kokoro-TTS, offline): im Workflow-Menü „Kokoro-Stimme"
  wählen → Text tippen → gesprochene Sprachnachricht direkt im Chat. Stimme
  wählbar (weiblich/männlich, warm/klar/britisch/tief).
- **Album-Cover zum Song:** beim Musik-Generieren fragt Qwirbel „Cover dazu?" –
  auf Wunsch malt er vorher ein passendes Cover (z-image) und liefert Cover + Song
  zusammen. Songs erscheinen als **Sprachnachricht** mit Play + Download.
- **Preset-Menü im Workflow-Chip:** Auflösung (480p/720p bzw. 640/1024/1344),
  Video-Länge (1–15 s) und FPS direkt wählen – oder nichts anfassen, dann wählt
  Qwirbel wie bisher automatisch. Musik-Länge (5–240 s) ebenso einstellbar.
- **Workflow in ComfyUI öffnen:** im Workflows-Tab je Workflow ein „ÖFFNEN"-Knopf,
  der ComfyUI im Browser aufmacht.

## v1.1.4 (Musik-Generierung & Windows-Aktivierung gefixt)
- **Musik generieren** (ACE-Step 1.5): unten in der Chat-Leiste bei der
  Workflow-Auswahl „Musik" wählen → zwei Felder wie bei Suno (oben **Styles**:
  Genre/Instrumente/BPM, unten **Lyrics** mit `[Verse]`/`[Chorus]`), fertiger
  Song als Audio-Player direkt im Chat.
- **Windows: Aktivierung gefixt.** Die Geräte-Kennung war unter Windows nicht
  stabil (mehrere Netzwerk-Adapter) → die Aktivierung konnte fehlschlagen,
  obwohl der Schlüssel stimmte. Sie wird jetzt fest gemerkt, dadurch klappt die
  Freischaltung zuverlässig. Aktivierungs-Fehlermeldungen sind jetzt klar
  (falscher Schlüssel-Typ / keine Verbindung / Gerät) statt kryptisch.

## v1.1.3 (ComfyUI-Feintuning & Chat-Zwischenantworten)
- Neue VRAM-Presets **8 GB / 12 GB** für schwächere Grafikkarten (kleiner &
  kürzer, ComfyUI-Cache aus = weniger RAM) – neben 16 GB und 32 GB.
  Settings → ComfyUI/VRAM.
- Neuer Schalter **„Alles entladen"**: nach der Generierung werden alle Modelle
  komplett aus dem Speicher geworfen (auch das Sprachmodell) → maximal RAM/VRAM
  frei; der erste Chat danach lädt kurz nach.
- **NVIDIA**-Karten: Qwirbel startet ComfyUI jetzt mit `--reserve-vram 0.6`
  (Puffer gegen „out of memory", lässt Speicher für Chat/Desktop frei).
- Beim Bild-/Video-Generieren zeigt der Chat jetzt eine **blaue Aktions-Zeile**
  mit dem fertigen Prompt und danach eine klare Bestätigung – man sieht genau,
  was Qwirbel gerade tut.

## v1.1.2 (Stabilität, Offline & Datenschutz)
- Speicher-Leck behoben: bei langen Aufgaben lief der Arbeitsspeicher nicht mehr
  voll – kein „schwarzer Bildschirm" / Absturz mehr mitten in der Aufgabe.
- Leerlauf-Speicher massiv gesenkt: das Sprachmodell (Whisper) lädt erst beim
  ersten Diktat, nicht mehr schon beim Start. (Wer den ersten-Klick-Ruckler
  vermeiden will: config `stt.preload: true`.)
- Läuft jetzt komplett OHNE Internet: alle Oberflächen-Bausteine (React, Fonts …)
  sind eingebettet – vorher wurden sie aus dem Netz geladen (ohne Verbindung schwarz).
- Neuer Update-Tab: Update-Paket (.zip) wählen → sichert automatisch, spielt nur
  den neuen Programmcode ein (deine Config, Lizenz, Chats, Wissen bleiben) → Neustart.
- Flüssigkeit/FPS jetzt 60–240 (High-Refresh-Monitore), ohne dass Details
  verschwinden – merklich flüssiger im Vollbild.
- Normaler Chat nutzt von sich aus keine Werkzeuge mehr (erst wenn du sie über den
  Chip zuschaltest) – ruhiger und stabiler mit lokalen Modellen.
- Privacy-Scanner laufen sauber auf Linux UND Windows; jeder Tab zeigt seine Anbindung.
- Werkzeuge (MCP) robuster: keine verwaisten Hintergrund-Prozesse mehr, saubere
  Fehlermeldung statt Absturz bei ungünstig geplanten Aufrufen.
- Ein einzelner Anzeigefehler kann nie mehr die ganze App schwarz machen.

## v1.1.0 (Chat-Upgrade: Cloud-Modelle & Werkzeuge)
- EIN Modell-Menü wie in der Ollama-App: Claude, Gemini, GLM & Co. stehen
  (mit eigenem API-Key, Settings → APIs) direkt neben den lokalen Modellen.
- Cloud-Modelle fahren jetzt auch Aufgaben, Planung und MCP-Werkzeuge –
  Bild-/Video-Generierung bleibt immer lokal auf deinem PC.
- MCP-Werkzeuge wirken jetzt im normalen Chat: „Wie spät ist es in Tokio?“
  nutzt automatisch das Zeit-Werkzeug. Aktivierte Server laufen automatisch
  mit (abschaltbar: config mcp.auto_im_chat), der MCP-Chip wählt enger aus.
- Denken-Schalter im Modell-Menü (qwen3 & Co., wie in der Ollama-App).
- Bestätigte Pläne laufen über denselben KI-Anbieter wie die Planung
  (vorher: stiller Rückfall auf das lokale Modell).

## v1.0.0 (Erstveröffentlichung)
- Lokaler KI-Assistent: Chat, autonomer Agent, Bild-/Video-/Sprach-Generierung.
- Automatik-Tab mit Pixel-Welt (wiederkehrende Aufgaben nach Zeitplan).
- Leben-Tab (Kalender, Aufgaben, Einkauf, E-Mail-Scan), Wissen & Profile.
- Server-Variante: Mehrbenutzer, Rollen, Rechte/Limits je Konto, Flotte, Audit.
- Android-Begleit-App (PC-Screen-Mirror + Fernsteuerung).
- Lizenz: Online-Aktivierung (einmalig), danach dauerhaft offline.
  Updates behalten die Aktivierung.
- Setup-Wizard fragt deinen Namen – die KI kennt dich persönlich.
- Speicher-Automatik: Bild-/Video-Modelle werden nach jeder Generierung
  komplett entladen – Chat bleibt flüssig, keine Speicher-Abstürze.

## 2026-08-15 – Leak-Scan erweitert um neue Build-Zielordner (Autonom-Task)

**Angepasst: scripts/make_release_windows.py** (950 → 1005 Zeilen; bestehendes `leak_scan()` WEITERGENUTZT, nichts neu geschrieben):
- Konstanten nach `VERSION` (~Z. 24): `BUILD_ZIELE = ["android-app", "ios-app", "docker", "helm", "exports"]` + `LEAK_SCAN_DATEIEN` (konfigurierbare Liste relativer Dateipfade, deren Vorkommen je Ziel zusätzlich namentlich geprüft wird).
- NEU `scanne_build_ziele() -> bool` (~Z. 733, direkt nach `leak_scan`): scannt JEDES Ziel aus `BUILD_ZIELE` einzeln mit derselben `leak_scan()`-Logik plus `LEAK_SCAN_DATEIEN`-Prüfung; druckt pro Ziel EINE Zeile (Dateien geprüft / Fundstellen / sauber); leere Ziele werden ehrlich als „0 Dateien geprüft“ ausgewiesen; Rückgabe False bei Funden → Aufrufer bricht hart ab wie bisher.
- Verifiziert 15.08. ~23:26 mit venv-Python: Syntax + Import OK. Testlauf von `scanne_build_ziele()`: ios-app 11 Dateien ✅ · docker 5 ✅ · helm 12 ✅ · exports 0 ✅ · android-app 611 Dateien ❌ **128 Fundstellen** = echte Altlasten im QUELL-Ordner (local.properties, .gradle/*-Error-Logs, .idea/workspace.xml mit ‚rumann', app/build/*). Diese Ordner sind im Verkaufs-Packer bereits über SEG_EXCLUDES draußen – Befund bedeutet: android-app als Quellordner nie ungefiltert weitergeben/verkaufen.
- Für die Mac/Linux-Helfer: Es gibt KEIN separates Leak-Scan-Skript – der Scan ist `leak_scan()` in **scripts/make_release_windows.py Z. 681–730**; genauso wiederverwenden (kleines, unabhängiges Eigenleben: `scripts/mache_web_demo.py` Z. 117; `backend/tools/privacy_actions.py` Z. 610 ist ein E-Mail-Check, nicht der Release-Scan).
