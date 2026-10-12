---
description: Backlog nach Linear umziehen – Verbindung prüfen, Team und Projekt wählen, Issues übertragen; danach liegen die Issues in Linear statt in docs/BACKLOG.md
argument-hint: "[Team-Kennung, optional – z. B. LEI]"
---

Wir ziehen den Backlog nach Linear um. Team: $ARGUMENTS (wenn leer: fragen, sobald die Verbindung steht).

**Leg in Linear nichts an und ändere keine Datei, bevor ich in Schritt 3 ausdrücklich zugestimmt habe.** Lesen ist erlaubt.

1. **Verbindung prüfen.** Lies über den Linear-MCP, womit du verbunden bist: Workspace, Teams (Name und Kennung), mein Benutzername. Gibt es keinen Linear-MCP oder bin ich nicht angemeldet, erklär es mir in drei Schritten und hör dann auf: `/plugin install linear@claude-plugins-official` (falls das Plugin fehlt), Claude neu starten, `/mcp` → *plugin:linear:linear* → *Authenticate* und im Browser mit dem Konto anmelden, mit dem ich in Linear eingeladen bin. Steht in `docs/BACKLOG.md` schon „Issues: Linear“, ist der Umzug erledigt: Sag mir Team und Projekt aus der Zeile, prüf nur, ob Issues aus der Tabelle dort in Linear fehlen, und hör auf.
2. **Team und Projekt.** Gibt es ein Team, frag, ob es das richtige ist; gibt es mehrere, frag, welches. Lies `docs/PRODUKT.md`: Gibt es im Team schon ein Projekt mit dem Produktnamen, nimm es; sonst schlag vor, eines mit diesem Namen anzulegen. Ohne Brief kein Projekt. Prüf die Status des Teams: Fehlt „In Review“, sag mir, dass ich ihn in Linear unter *Settings → Teams → [Team] → Issue statuses* bei *Started* anlegen kann – kein Grund aufzuhören.
3. **Zuordnung zeigen.** Lies `docs/BACKLOG.md`. Zeig mir eine Tabelle: Nummer in der Datei, Titel, Status in Linear (⬜ offen → Todo, 🔧 in Arbeit → In Progress, ✅ fertig → Done). Such für jeden Titel im Team nach einem Issue mit gleichem oder fast gleichem Titel und markier es mit „gibt es schon: [Kennung]“ – das wird nicht angelegt. Ideen unter „Später“ im Brief bleiben im Brief. Frag, ob das so stimmt.
4. **Erst nach meinem Okay anlegen.** Pro Issue in der Tabelle: Titel, Beschreibung mit den vier Überschriften **Ziel**, **Nicht im Umfang**, **Akzeptanzkriterien**, **Fertig, wenn** – Wortlaut aus der Datei, Kriterien als Liste –, der Status aus der Tabelle, das Projekt aus Schritt 2, niemandem zugewiesen. Merk dir jede Kennung. Bricht ein Anlegen ab, versuch es nicht einfach noch einmal: erst nachsehen, ob es das Issue inzwischen gibt.
5. **Dateien umstellen** (gehört zum Okay aus Schritt 3):
   - `docs/BACKLOG.md`: Die drei Kopfzeilen bleiben. Darunter statt der Issues genau diese Zeile: `Issues: Linear · Team [Kennung] · Projekt [Name]` (ohne Projekt: nur Team), dann die Adresse des Teams in Linear und eine Tabelle alte Nummer → Kennung. Die alten Issue-Texte entfallen – sie stehen jetzt in Linear und im Git-Verlauf.
   - `docs/PRODUKT.md`, Abschnitt 5: hinter jedes MVP-Stichwort die Kennung in Klammern.
   - `CLAUDE.md`: Fehlt der Abschnitt „Issues in Linear“, häng ihn vor den Zeilen an, die mit `@` beginnen – Wortlaut unten. Ändere sonst nichts an `CLAUDE.md`.
   - `docs/ENTSCHEIDUNGEN.md`: eine Zeile mit heutigem Datum: „Issues liegen in Linear, Team [Kennung] — Backlog im Team statt in der Datei“.
6. **Abschluss.** Zeig mir die Kennungen mit Titel. Bitte mich, sie in Linear kurz anzusehen. Sag: Als Nächstes `/ndu-commit`, danach startet ein Issue mit „Setze [Kennung] um“. Führ `/ndu-commit` nicht selbst aus.

Abschnitt für `CLAUDE.md` (nur, wenn er fehlt):

```
## Issues in Linear

Steht in `docs/BACKLOG.md` „Issues: Linear“, liegen die Issues in Linear und nicht in der Datei. Dann gilt:

- Ein Issue holst du per Kennung (z. B. LEI-5) über den Linear-MCP – nie aus dem Gedächtnis. Ist der MCP nicht verbunden, sag es und erklär: `/mcp` → *plugin:linear:linear* → *Authenticate*.
- Zu Beginn: Status In Progress, der angemeldeten Person zugewiesen. Arbeitest du auf einem Branch, beginnt sein Name mit der Kennung in Kleinbuchstaben (z. B. `lei-5-beschreibung`).
- Am Ende: die Belege je Kriterium zusätzlich als Kommentar ins Issue. Gibt es einen Pull Request, kommt sein Link in den Kommentar und das Issue auf In Review (gibt es den Status nicht, bleibt es auf In Progress). Done erst, wenn die Person „fertig“ sagt – arbeitet ein Team im Repo, erst nach dem Zusammenführen.
- Anlegen nur nach gezeigter Liste und Okay, vorher nach gleichem Titel suchen. Format der Beschreibung: Ziel, Nicht im Umfang, Akzeptanzkriterien (Gegeben … wenn … dann …), Fertig, wenn.
- Nie löschen – stattdessen Canceled mit einem Kommentar, warum. Nie Issues ändern, die jemand anderem zugewiesen sind.
- `docs/PRODUKT.md` und `docs/ENTSCHEIDUNGEN.md` bleiben im Repo; Ideen für Später stehen im Brief, nicht in Linear.
```

Sprache: Deutsch, einfache Worte, keine Fachbegriffe ohne kurze Erklärung.
