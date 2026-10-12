---
description: Strenge Prüfung mit frischem Blick – ein Subagent prüft Secrets, Zugriffsregeln (RLS), Eingaben und was Fremde sehen; du entscheidest, was behoben wird
argument-hint: [Bereich, optional – z. B. „nur die Tabelle anfragen“]
---

Lass das Projekt von jemandem prüfen, der den Code nicht geschrieben hat. Bereich: $ARGUMENTS (wenn leer: das ganze Projekt).

1. **Auftrag schreiben.** Für den Prüfer, ohne dieses Gespräch verständlich: das Produkt in einem Satz (aus `docs/PRODUKT.md`), die Issues mit Status „fertig“ oder „in Arbeit“ aus `docs/BACKLOG.md`, die Regeln zu Keys und Datenbank aus `CLAUDE.md`. Fehlt der Brief oder ist noch kein Issue fertig, prüft er, was im Code schon da ist.
2. **Prüfen lassen.** Starte damit einen Subagenten vom Typ **Plan** (Agent-Werkzeug: `subagent_type: Plan`, kein anderes Modell angeben). Er darf lesen, suchen und über den Supabase-MCP Tabellen und Regeln lesen (ist der MCP nicht verbunden, nur den Code – und das sagst du im Bericht) – aber nichts verändern: keine Datei, kein Commit, kein SQL, das schreibt. Er prüft in dieser Reihenfolge und hört nach 5 Funden auf:
   - **Secrets:** ein Key im Code oder in Git; ein `sb_secret_`-, anon- oder service_role-Key, der über `NEXT_PUBLIC_` im Browser landet.
   - **Zugriffsregeln:** jede Tabelle mit RLS eingeschaltet und je Operation eine Regel; Schreib-Regeln, die allen alles erlauben; Spalten wie E-Mail, die Fremde lesen können.
   - **Eingaben:** Was ein Formular schickt, prüft auch der Server (leer, zu lang, fremde IDs).
   - **Fremde:** ohne Login, ohne Daten, bei einem Fehler – weiße Seite oder ein verständlicher Satz?
   Nicht melden: Stil, Aufräumen, alles, was niemand im Browser merkt.
3. **Berichten.** Pro Fund eine Zeile, ohne Fachjargon: was eine fremde Person damit tun könnte, wo (Datei oder Tabelle), und **Muss** (vor dem nächsten Push) oder **Kann warten**. Ist ein Fund unsicher, schreib „Frag Markus“ statt zu raten. Keine Code-Blöcke. Nichts gefunden: ein Satz – plus, was noch nicht prüfbar war (z. B. keine Datenbank verbunden, noch kein Formular).
4. **Erst nach meinem Okay beheben** – nur die Punkte, die ich freigebe. Danach `npm run lint`, `npm run build` und zu jedem Punkt ein Beleg; bei Zugriffsregeln der Test als fremde Person (Rolle anon und authenticated, jeder Versuch in einer Transaktion, die du zurückrollst). Dann sag: im Browser prüfen, `/ndu-check`, `/ndu-commit`. Führ sie nicht selbst aus.

Nutze nie das Modell Fable oder `best` – das kostet im Pro-Plan extra.
