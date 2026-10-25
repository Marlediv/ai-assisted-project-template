# Entscheidungen zu den offenen Punkten O-01 bis O-09

**Bezug:** `lastenheft-v1.0.md`, Kapitel 11 (Branch `docs/lastenheft-v1.0`)
**Status:** Vorgeschlagen und festgelegt für die Baseline-Vorbereitung. **PO-Bestätigung ausstehend.**
Die Entscheidungen gelten erst mit der PO-Freigabe der Baseline.

Die Entscheidungen wurden vom Assistenten auf Auftrag des Projektverantwortlichen erarbeitet.
Punkte, die nur durch einen technischen Test verifiziert werden können, sind als solche markiert.

---

## O-01: Verbindliche MVP-Mussliste

**Entscheidung:** Die Mussliste aus Kapitel 9.1 wird übernommen. Sie wird um folgende Präzisierung ergänzt:

- Das Dashboard enthält im MVP alle in F-017 genannten Operationen: Status, Start, Pause, Fortsetzen, Abbruch und Freigabe.
- Benachrichtigungen (F-014) und vollständiges Onboarding (F-016) sind **Soll**, nicht Muss.
- Die Reihenfolge der Ausbaustufen entspricht Kapitel 9.2 (A, dann B, dann C).

**Begründung:** F-017 ist bereits beschlossen. Eine Reduktion des Dashboards würde gegen diese Entscheidung verstoßen.

---

## O-02: Freigabematrix

**Entscheidung:** Stufenmodell mit drei Klassen.

| Aktion | Klasse | Hinweis |
|---|---|---|
| Lesen im Projekt | Frei | |
| Schreiben im Auftrags-Worktree | Frei | |
| Lokale Tests und Quality Gates ausführen | Frei | |
| Push, Pull Request | Freigabepflichtig | |
| Netzwerkzugriffe | Freigabepflichtig | Ausnahme: lokale Dienste ohne externe Ziele |
| Abhängigkeiten installieren | Freigabepflichtig | |
| Löschen von Dateien | Freigabepflichtig | |
| Schreiben außerhalb des Worktrees | Freigabepflichtig | |
| Schreiben auf den stabilen Branch | Verboten | Nur über die Integration nach PO-Freigabe (F-019) |
| Zugriff auf Secrets | Verboten | Siehe O-08 |

**Begründung:** Die Klassen folgen F-003 (risikobasierte Autonomie) und A-04 (Freigabegrenzen).

---

## O-03: Technische Durchsetzbarkeit der Berechtigungen

**Entscheidung:** Kombination aus CLI-Mechanismen und, sofern nötig, Betriebssystem-Isolation. Die genaue Ausprägung hängt vom Ergebnis des Machbarkeitstests ab.

**Regel, die unabhängig vom Testergebnis gilt:** Ist eine Beschränkung nicht technisch durchsetzbar, wird die Aktion blockiert. Eine ungeschützte Ausführung findet nicht statt (A-08).

**Status:** *Technisch zu verifizieren.* Vor Baseline-Freigabe ist ein Machbarkeitstest mit Claude Code und Codex CLI durchzuführen. Die Negativfälle aus T-09 (Datei-, Netzwerk- und Toolzugriff) sind dabei als Prüfkriterien zu verwenden.

**Begründung:** Ob eine Sandbox greift, lässt sich nur am realen Werkzeug prüfen, nicht durch Festlegung.

---

## O-04: Betriebssysteme und CLI-Versionen

**Entscheidung:**
- **MVP:** macOS und Linux.
- **Später:** Windows (Ausbaustufe C).
- CLI-Versionen werden festgelegt (gepinnt) und dokumentiert. Die Version, mit der getestet wurde, ist Teil des Testnachweises.

**Begründung:** Die Entwicklungsumgebung ist macOS. Linux deckt typische Server- und CI-Umgebungen ab. Windows erhöht den Testaufwand deutlich.

---

## O-05: Auftragszustände, Retry und Idempotenz

**Entscheidung:** Zustandsmaschine aus Kapitel 8 mit einem Mindestset an Zuständen und expliziten Übergängen.

**Mindestset:** Entwurf, freigegeben, eingeplant, in Planung, in Implementierung, in Test, im Review, Nachbesserung, wartet auf Freigabe, blockiert, pausiert, integrationsbereit, in Integration, abgeschlossen, fehlgeschlagen, abgebrochen.

**Sichere Haltepunkte** (Wiederaufnahme nur hier):
- nach abgeschlossenem Plan,
- nach abgeschlossener Implementierung im Worktree,
- nach abgeschlossenem Review,
- nach Vorliegen eines Gate-Ergebnisses.

**Idempotenz:** Nicht idempotente Aktionen (Push, Integration) werden vor einem Retry zuerst auf ihren tatsächlichen Stand geprüft. Ein Retry erfolgt nur, wenn die Aktion nachweislich nicht ausgeführt wurde (A-03).

---

## O-06: Standardlimits

**Entscheidung:** Konfigurierbare Standardwerte, pro Projekt und pro Auftrag überschreibbar. Die folgenden Werte sind **Startwerte für den Pilot** und keine geprüften Grenzen.

| Limit | Startwert |
|---|---|
| Review-Korrekturzyklen je Auftrag | 3 |
| Laufzeit je Agentenlauf | 60 Minuten |
| Wiederholungen eines fehlgeschlagenen Laufs | 2 |
| Gesamtbudget je Auftrag | Pflichtfeld, kein Standardwert |

**Eskalation:** Nach Erreichen eines Limits wird der Auftrag auf „wartet auf Freigabe“ gesetzt. Es erfolgt kein stiller Abbruch und kein weiterer Versuch (F-023, T-08).

**Begründung:** Es fehlen Messdaten. Die Werte werden im Pilot (T-15) kalibriert.

---

## O-07: Vorrang der Richtlinien

**Entscheidung:** Die restriktivste Regel gewinnt: global, dann projektbezogen, dann auftragsbezogen.

Eine Lockerung einer übergeordneten Regel ist nur mit ausdrücklicher PO-Entscheidung zulässig und wird in der Historie dokumentiert.

**Begründung:** Entspricht F-003 und F-026. Ein Auftrag darf eine Schutzregel nicht stillschweigend aufheben.

---

## O-08: Secrets, Datenschutz und Aufbewahrung

**Entscheidung:**
- **Redaktion ist Pflicht** in Logs, Dashboard, Benachrichtigungen und Agentenausgaben (N-004).
- **Keys und Tokens** werden nur über Umgebungsvariablen oder den Schlüsselbund des Betriebssystems bereitgestellt. Sie stehen nie in Projektdateien, Auftragsdaten oder der Historie.
- **Speicherung** der Daten erfolgt lokal.
- **Aufbewahrung** der Ausführungshistorie: Standard 90 Tage, pro Projekt konfigurierbar.
- **Zugriffsschutz:** Das Dashboard läuft nur auf `localhost` und ist nicht ohne Authentifizierung über das Netzwerk erreichbar.

**Status:** Die Aufbewahrungsfrist von 90 Tagen ist eine Annahme und sollte bestätigt werden.

---

## O-09: Git-Voraussetzung

**Entscheidung:** Git ist im MVP Pflicht. Beim Onboarding wird für Projekte ohne Git ein `git init` angeboten. Dies geschieht nur nach ausdrücklicher Freigabe.

Nicht versionierte Projekte mit Snapshot-Lösung sind ein Ausbaupunkt (Stufe A oder später).

**Begründung:** Worktrees setzen Git voraus (F-018). Die Snapshot-Lösung wäre ein eigener Funktionsumfang.

---

## Offene Prüfungen vor Baseline

1. Machbarkeitstest der Berechtigungen (O-03) mit Claude Code und Codex CLI.
2. PO-Bestätigung aller Entscheidungen oben.
3. Anpassung von Kapitel 11 des Lastenheft-Entwurfs auf „entschieden“ je Punkt, mit Verweis auf dieses Dokument.
4. Unabhängiges Codex-Review der konsolidierten Fassung (Kapitel 14, Schritt 4).
