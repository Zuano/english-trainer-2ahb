# Plan: Englisch-Lern-Web-App (Schularbeit 2. Semester, 2AHB)

## Ziel

Eine motivierende Lern-Web-App nach der **Birkenbihl-Methode**, kombiniert mit Christians **Pick-and-Build-Prinzip** (nie tippen, immer per Dropdown wählen). Deckt den kompletten Schularbeitsstoff ab, mit englischem Audio von ElevenLabs.

## Entschieden

| Frage | Entscheidung |
|---|---|
| Audio | Vorab generierte MP3s (ElevenLabs, nur englischer Text) – kein API-Key in der App |
| Login | Keiner nötig (Key-Problem entfällt durch vorab generiertes Audio) |
| Umsetzung | Direkt hier in Cowork (statische Web-App, kein Claude Code nötig) |
| Reihenfolge | Kernthemen zuerst, Rest danach |
| **Schularbeit** | **19. Juni 2026 → 7 Tage Zeit** |
| Aufgaben-Quelle | **Zuerst alle Aufgaben der Professorin lösen** (Lösungsschlüssel erstellen, mit Key_Practice.pdf und teacher-Versionen abgleichen), dann als Übungs- und Prüfungsaufgaben in die App übernehmen |
| ElevenLabs-Key | Erhalten ✓ – liegt nur temporär in Claudes Arbeitsumgebung, kommt nie in App/Ordner/ZIP. Nach Audio-Generierung rotieren. |

## Stoff-Inventar (aus dem Ordner)

1. **(Social) Media + Fake News** ← von der Professorin bestätigt (Reading „Traditional Media and New Media", Fake-News-Worksheet, Media Vocabulary, Blog Entry Aufgabe)
2. **Conditionals I, II, III**
3. **Reported Speech**
4. **Passive**
5. Modal Verbs
6. Prepositions (verb + preposition)
7. Quantifiers
8. Shopping (Vocabulary)
9. Music (Unit-Auszug)
10. Presentation (Useful Phrases)

Dazu: Blog-Post-Anleitung (Textsorte) und Key_Practice.pdf (Lösungen) als Quellen.

**Phase 1 (Kern):** Themen 1–4 + Textsorte Blog Entry. **Phase 2:** Themen 5–10.

## App-Konzept

Eine statische Web-App: `index.html` + `audio/`-Ordner. Vanilla JS, kein Framework, läuft lokal und auf jedem Hoster. Fortschritt wird im Browser gespeichert (localStorage).

### Navigation

Tabs pro Thema. Innerhalb jedes Themas drei Bereiche:

**1. Lesen & Hören (Birkenbihl)**
- Englischer Text, satzweise dargestellt
- Unter jedem Satz: **Wort-für-Wort-Dekodierung** (jedes englische Wort mit deutscher Entsprechung direkt darunter, Birkenbihl-Stil)
- Darunter ausklappbar: **sinnvolle deutsche Übersetzung** des Satzes
- ▶-Button pro Satz und „Ganzen Text abspielen" – nur Englisch wird vorgelesen, nie die Übersetzungen
- Übersetzungen einzeln ein-/ausblendbar (Stufe 1: alles sichtbar → Stufe 3: nur Englisch = Lernfortschritt)

**2. Üben (Pick and Build)**
- Alle Aufgaben per **Dropdown**: eine richtige + mehrere plausible falsche Antworten, nichts wird getippt
- Nach Auswahl erscheint die Wort-für-Wort-Übersetzung des gewählten Worts/Chunks
- Sofortiges Feedback (grün/rot), **„Lösung anzeigen"-Button bei jeder Aufgabe**
- Aufgabentypen je nach Thema:

| Thema | Übungstypen |
|---|---|
| Media/Fake News | Vokabel-Dropdowns (confirmation bias, mis-/disinformation…), Lückentexte aus dem Reading, Richtig/Falsch zum Text |
| Conditionals | Satz umformen: if-Satz Stück für Stück per Dropdown zusammenbauen (Typ 0–III), Typ erkennen |
| Reported Speech | Direkte Rede → indirekte Rede per Dropdown-Bausteine (Zeitverschiebung, Pronomen, Zeitangaben) |
| Passive | Aktiv → Passiv zusammenbauen (Form von be + past participle wählen) |
| Blog Entry | Struktur-Bausteine ordnen (Introduction/Main/Conclusion), passende informelle Phrasen wählen |

**3. Prüfungsmodus**
- Mix aus allen Übungen des Themas als „Mini-Schularbeit": erst am Ende Auswertung mit Punkten und Note
- Zusätzlich themenübergreifende Gesamtprüfung über alles

### Motivation / Erfolgserlebnisse

- Punkte pro richtiger Antwort, Fortschrittsbalken pro Thema und gesamt
- Konfetti/Animation bei abgeschlossenen Abschnitten, aufmunternde Meldungen
- Falsch beantwortete Aufgaben landen automatisch in „Nochmal üben"
- Themen-Badges („Conditionals gemeistert ✓")

## Audio-Pipeline (ElevenLabs)

1. Ich extrahiere alle englischen Texte und Übungssätze aus den PDFs
2. Build-Skript ruft die ElevenLabs-API auf (Modell eleven_multilingual/turbo, eine natürliche Stimme – du kannst aus 2–3 Vorschlägen wählen) und erzeugt **eine MP3 pro Satz** + Gesamttext-MP3s
3. MP3s landen in `audio/`, die App referenziert nur Dateien → **dein API-Key bleibt bei dir, ist nirgends in der App enthalten**

Was ich dafür brauche: deinen ElevenLabs-API-Key einmalig zur Generierung (danach löschbar) und deine Stimm-Präferenz (männlich/weiblich, britisch/amerikanisch).

## Weitergabe an Mitschüler

Ohne Login, zwei Optionen (beide möglich):
- **ZIP über Teams**: Ordner zippen, Mitschüler entpacken und öffnen `index.html` – funktioniert komplett offline
- **Netlify Drop / GitHub Pages**: kostenloser Link, immer aktuelle Version

## Arbeitsschritte (Stand 12.6. – alles am ersten Tag erledigt ✅)

1. ✅ Stoff sichten, Plan abstimmen
2. ✅ Alle Worksheets extrahiert (28 Dateien, 2× OCR) und ALLE Aufgaben gelöst – abgeglichen mit Key_Practice, teacher-Version (Conditionals) und modals_extension. Lösungs-Dokumente in `loesungen/`.
3. ✅ App gebaut: `index.html` + `content.js` – Tabs, Birkenbihl-Ansicht (3 Lernstufen), Dropdown-Engine mit Wort-für-Wort-Anzeige, Lösungs-Buttons, Punkte/Streak/Konfetti/Abzeichen, Prüfungsmodus mit Note, „Nochmal üben"-Pool. Komplett offline-fähig, automatisiert getestet.
4. ✅ Alle 11 Themen befüllt: **382 Aufgaben, 173 Birkenbihl-Sätze**
5. ✅ Audio: 173 MP3s mit ElevenLabs generiert (Stimme: Moritz Wegner, eleven_multilingual_v2) – nur englische Texte, satzweise + „ganzen Text anhören"
6. ✅ Klassen-Paket: `English-Trainer-2AHB.zip` (9,7 MB) – entpacken, index.html doppelklicken, fertig (siehe ANLEITUNG.txt)
7. ✅ Karaoke-Modus: Beim Vorlesen werden aktueller Satz + aktuelles Wort live hervorgehoben (echte ElevenLabs-Zeitstempel in `timings.js`)
8. ✅ Lernfortschritt erweitert: gehörte Sätze werden getrackt (grüner ▶-Button), Hör-Balken pro Text und Thema, Statistik-Dashboard auf der Startseite (Punkte, Streak, Themen-Abzeichen, Prüfungen)
9. ✅ **Buch-Tab (Nachtrag der Professorin, 12.6. abends):** Tab „📖 Buch (Schularbeit)" mit Untertabs Conditionals (S. 31), Modal Verbs (S. 57), Reported Speech (S. 89), Mixed Tenses (S. 126–127) – alle 95 Aufgaben von den Original-Buchseiten gelöst (gedruckte Seitennummern, Scans direkt gelesen), 12 vertonte Beispielsätze, Lösungen in `loesungen/buch.md`. Verteil-Pakete neu: ZIP aktualisiert, `github-upload-neu/` (3 Schritte). Engine kann jetzt generell Untertabs (auch im Skill).

## Offene Punkte

- **API-Key im ElevenLabs-Dashboard rotieren** (war im Chat sichtbar – Sicherheit!)
- Falls Moritz' englischer Akzent nicht gefällt: Stimme sagen → Neugenerierung dauert ~2 Min
- ZIP über Teams an die Mitschüler verteilen
- Optional Phase 3: Hosting (Netlify Drop) statt ZIP
