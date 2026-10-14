# Lastenheft: AI-Project-Toolkit

**Version:** 1.0 · Entwurf  |  **Stand:** 14.10.2026  |  **Freigabe:** AUSSTEHEND  
**Dokumenttyp:** Fachliches Lastenheft (Was/Warum; keine verbindliche Implementierungsarchitektur)  
**Product Owner:** Projektverantwortlicher  |  **Unabhängiges Codex-Review:** NICHT DURCHGEFÜHRT  
**Grundlage:** Bestätigte Entscheidungen des Anforderungsinterviews, frühere Projektgespräche und vorhandener Lastenheft-Entwurf vom 13.10.2026.

> **Wichtige Statusregel:** „Beschlossen“ bedeutet fachlich im Interview bestätigt, nicht implementiert oder als Lastenheft-Baseline freigegeben. „Vorgeschlagen“ bezeichnet eine aus Entscheidungen abgeleitete, noch zu bestätigende Ausgestaltung. „Offen“ erfordert weitere Klärung. Der MVP-Zuschnitt in Kapitel 9 ist ein Vorschlag, keine bereits genehmigte Release-Baseline.

## 1. Ausgangslage und Motivation

Das bestehende AI-Project-Toolkit ist ein wiederverwendbares Projekt-Template mit gemeinsamer Dokumentation und Anweisungen für KI-Entwicklungswerkzeuge. Der bisherige Entwicklungsprozess benötigt manuelle Übergaben zwischen Anforderungserhebung, Planung, Implementierung, Tests, unabhängigem Review und finaler Freigabe. Chatverläufe und CLI-Sitzungen bilden keine belastbare persistente Auftragssteuerung. Das neue Produkt soll diese Lücke schließen und als eigenständiger lokaler Orchestrator mit optionalen Integrationen dienen.

Die Nutzung von GitHub ist **optional**. Git als Versionsverwaltung und GitHub als Hosting-/Kollaborationsdienst sind ausdrücklich zu unterscheiden. Für den beschlossenen Git-Worktree-MVP wird ein lokales Git-Repository vorausgesetzt; die Unterstützung nicht mit Git versionierter Projekte ist noch nicht beschlossen.

## 2. Ziele und Nichtziele

**Z-001 · Kontrollierte autonome Entwicklung [BESCHLOSSEN].** Ein freigegebener Entwicklungsauftrag wird durch Agenten weitgehend autonom analysiert, geplant, implementiert, getestet, unabhängig geprüft und als nachvollziehbares Ergebnis zur PO-Entscheidung vorgelegt. Kritische Entscheidungen, relevante Umfangsänderungen und die finale Integration bleiben freigabepflichtig.

Weitere Ziele: nachvollziehbare Qualität, zuverlässige Wiederaufnahme, lokale und GitHub-unabhängige Nutzung, schrittweise Erweiterbarkeit auf mehrere Projekte, Modelle und parallele Aufträge, transparente Ressourcensteuerung sowie ein niedrigschwelliger Bedienzugang über CLI und Web-Dashboard.

**Nichtziele des MVP:** vollständig autonome Übernahme in den stabilen Branch ohne PO-Freigabe; zwingende GitHub-Anbindung; verpflichtende Cloud- oder Mehrbenutzerplattform; vollständige parallele Ausführung; vollständige automatische Selbstaktualisierung. Nichtziel bedeutet nicht, dass die Funktion als spätere Zielanforderung entfällt.

## 3. Beteiligte Rollen und Verantwortlichkeiten

| Rolle | Verantwortung | Status |
|---|---|---|
| Product Owner (PO) | Ziele, Prioritäten, verbindlicher Auftragsumfang, Ausnahme- und Integrationsfreigaben, Abnahme | Beschlossen |
| ChatGPT / Requirements Engineer | Fachliche Klärung, Strukturierung, Beratung und Entscheidungsvorlagen; kein autonomer Orchestrator | Beschlossen |
| Codex CLI | Analyse, Planung, projektmanagementbezogene Aufgaben, unabhängiges Review | Beschlossen |
| Claude Code CLI | Implementierung, Tests, Nachbesserung, technische Dokumentation | Beschlossen |
| Lokaler Orchestrator | Auftrags- und Zustandsverwaltung, Ereignisse, Berechtigungen, Ressourcen, Übergaben, Nachweise | Beschlossen |
| Weitere Rollen | Fachliche Beteiligte, spätere Nutzer- und Rechteverwaltung | Offen |

Der Orchestrator muss ohne aktive ChatGPT-Sitzung weiterarbeiten. Ein durch Claude Code implementierter Stand darf nicht durch denselben Implementierungsschritt als unabhängig abgenommen gelten.

## 4. Fachlicher Sollprozess

1. Projekt registrieren und dessen Regeln/Umgebung feststellen.
2. Entwicklungswunsch in strukturierten Auftrag mit Zielen, Grenzen, Risiken und testbaren Akzeptanzkriterien überführen.
3. PO bestätigt den verbindlichen Auftragsstand und gibt die autonome Bearbeitung frei.
4. Orchestrator prüft Berechtigungen, Ressourcen, Abhängigkeiten und Arbeitsbereich.
5. Codex analysiert und plant die Umsetzung.
6. Claude Code implementiert, testet und aktualisiert relevante Dokumentation im isolierten Arbeitsbereich.
7. Codex prüft unabhängig; Befunde führen zu kontrollierten Korrekturen, Neuplanung oder Eskalation.
8. Quality Gates liefern nachweisbare Ergebnisse; Freigabeanfragen blockieren nur betroffene/abhängige Schritte.
9. PO prüft Änderungsstand, Risiken, Tests und Review und entscheidet über die Integration.
10. Orchestrator prüft den freigegebenen Stand erneut, integriert bei gültiger Freigabe und dokumentiert das Ergebnis.
11. Auftrag und Historie bleiben persistent; bei Blockade kann ein anderer ausführbarer Auftrag aus der Warteschlange starten.

## 5. Anforderungskatalog: fachlich bestätigte Anforderungen

Die IDs entsprechen den im laufenden Interview vergebenen Kennungen; sie sind **nicht** mit den anders nummerierten IDs des älteren Lastenheft-Entwurfs gleichzusetzen. Die Zuordnung zu MVP/Später ist in Kapitel 9 als *Vorschlag* dargestellt.

### 5.1 Produktstrategie und Grundlagen

| ID | Beschlossene Anforderung | Prüfbarer Kernnachweis |
|---|---|---|
| R-001 | Lokal zuerst, spätere Remote-/Cloud-Worker möglich | Lokal ohne Remote-Dienst lauffähig; Ausführung von Steuerung entkoppelt |
| R-002 | Stufenweise Entwicklung mit nutzbarem MVP | Erste Stufe führt echten vollständigen Entwicklungsauftrag durch |
| R-003 | MVP mit Muss-Kriterien und Erweiterungsoptionen | Genehmigter Muss-Katalog und eigene Abnahmekriterien; Änderungen nur per PO-Entscheid |
| P-001 | Strukturierte Abschlussprüfung vor Lastenheft-Freigabe | Konsolidierung, Konsistenzcheck, MVP-Abgrenzung, offener-Punkte-Klärung, unabhängiges Codex-Review, PO-Freigabe |

### 5.2 Workflow, Aufträge und Agenten

| ID | Beschlossene Anforderung | Prüfbarer Kernnachweis |
|---|---|---|
| F-002 | Persistente Zustände, sichere Wiederaufnahme und Retry-Strategie | Neustart erhält Entscheidungen und Status; keine unkontrollierte Doppelaktion |
| F-003 | Risikobasierte Autonomie | Risikoarme erlaubte Schritte autonom; Architektur-/Scope-/Sicherheitsänderungen und finale Abnahme PO-pflichtig |
| F-004 | Ereignisgesteuerter Orchestrator | Zustandsübergänge und Übergaben sind nachvollziehbar und validiert |
| F-005 | ChatGPT als fachliche PO-Schnittstelle | Status-/Entscheidungsunterstützung; Orchestrator funktioniert ohne offene Chatsitzung |
| F-006 | GitHub-unabhängige kanonische Auftragsverwaltung | Auftrag lokal anlegen, verfolgen und abschließen; GitHub optional |
| F-007 | Codex-Planung/Review und Claude-Implementierung/Tests in kontrollierten Zyklen | Echte CLI-Aufrufe, getrennte Rollen, Review-Befunde und Korrekturen nachweisbar |
| F-008 | Risikobasierte Quality Gates | Pflichtprüfungen verhindern Freigabe bei Fehlschlag; PO-Ausnahmen dokumentiert |
| F-009 | Parallele Entwicklung als Zielanforderung | Später unabhängige isolierte Aufträge mit Abhängigkeiten und Integrationskontrolle |
| F-010 | Regelbasierte Modellwahl nach Rolle, Risiko, Aufgabe und Limits | Modellentscheidung folgt konfigurierbaren Vorgaben und wird protokolliert |
| F-011 | Qualitätsgesicherter Modell-Fallback | Nur geeignete freigegebene Alternativen; gepinnte Modelle nicht stillschweigend ersetzen |
| F-012 | Modellprofile mit Ergebnisauswertung | Review-/Test-/Retry-Ergebnisse fließen in nachvollziehbare Bewertung ein, ohne eigenmächtige Regeländerung |
| F-020 | Asynchrone Freigaben für betroffene Schritte | Abhängige Schritte blockiert, unabhängige Schritte dürfen weiterlaufen; Entscheidungen persistent |
| F-021 | KI-gestützte strukturierte Auftragsdefinition | Ziel, Scope, Kriterien, Einschränkungen, Risiken; PO bestätigt Version vor Start |
| F-022 | Kontrollierte Änderungen laufender Aufträge | Änderungsantrag, Folgenanalyse, neue Version, erneute PO-Freigabe und Revalidierung |
| F-023 | Fortschrittsabhängige Fehlerbehandlung und Eskalation | Fehlerarten, Fortschritt und Limits berücksichtigt; keine Endlosschleife |
| F-028 | MVP: sequenzielle Auftragsausführung mit persistenter Warteschlange | Mehrere Aufträge verwaltbar, höchstens ein aktiv ausgeführter Auftrag, Neustart sicher |
| F-029 | Blockierter Auftrag gibt Ausführungsplatz frei | Blockade persistiert; nächster ausführbarer Auftrag startet; später sichere Wiedereinplanung |

### 5.3 Bedienung, Projekte, Ressourcen und Nachweise

| ID | Beschlossene Anforderung | Prüfbarer Kernnachweis |
|---|---|---|
| F-013 | Lokales Dashboard und CLI mit gemeinsamem Zustand | Beide bedienen dieselben Aufträge; Browser schließen stoppt keine Ausführung |
| F-014 | Konfigurierbare Benachrichtigungen | Freigaben, Blockaden, kritische Fehler und Abschluss meldbar; Duplikate vermieden |
| F-015 | Zentrale Verwaltung mehrerer isolierter Projekte | Projektzustände, Regeln, Aufträge und Workspaces getrennt; Ressourcen global koordiniert |
| F-016 | Geführtes Onboarding für neue/bestehende Projekte | Analyse und Einrichtungsvorschlag; keine Überschreibung ohne Freigabe |
| F-017 | MVP: CLI plus schlankes lokales Web-Dashboard | Aufträge starten, Status/Agenten/Fehler sehen, freigeben, pausieren, fortsetzen, abbrechen |
| F-018 | Isolierte Git-Branches und Worktrees je Entwicklungsauftrag | Stabiler Branch bleibt bis zur freigegebenen Integration unangetastet |
| F-019 | Automatische Integration nach ausdrücklicher PO-Freigabe | Freigabe bindet Änderungsstand und Zielbranch; Konflikt/Änderung erfordert Revalidierung |
| F-024 | Ressourcenmanagement auf Auftrags-, Projekt- und Systemebene | Limits/Warnungen/Blockaden; gemessene, geschätzte und unbekannte Werte getrennt |
| F-025 | Strukturierte und verständliche Ausführungshistorie | Ereignisse, Modellwahl, Reviews, Tests, Änderungen, Freigaben und Artefakte zuordenbar |
| F-026 | Automatische Dokumentationspflege mit unabhängigem Review | Code und Dokumentation im selben Änderungsstand; Policy-Änderung nicht eigenmächtig |
| F-027 | Kontrollierte Updates mit Zustandsübernahme | Kompatibilitätsprüfung, sicherer Stopp, Sicherung/Migration/Validierung und Wiederherstellung |

### 5.4 Sicherheit und Abnahme

| ID | Beschlossene Anforderung | Prüfbarer Kernnachweis |
|---|---|---|
| S-001 | Zentrale, technisch durchsetzbare Berechtigungsrichtlinien | Projekt-/Auftragsregeln für Datei, Shell, Netzwerk, Tools; unzulässige Aktion wird blockiert |
| Q-001 | Szenariobasierte MVP-Abnahme | Automatisierte Tests plus E2E-, Fehler-, Freigabe-, Wiederanlauf- und Sicherheitsfälle |
| Q-002 | Testprojekt und reales Pilotprojekt | Kontrollierte Reproduktion plus echter begrenzter Auftrag; dokumentierte PO-Abnahme |

## 6. Detaillierte übergreifende Akzeptanzbedingungen

**A-01 Auftragsfreigabe:** Ein Auftrag ohne PO-bestätigte Auftragsversion darf nicht in die Implementierung übergehen. Die Freigabe referenziert die konkrete Version.

**A-02 Agentenübergabe:** Codex erzeugt einen überprüfbaren Plan. Claude Code implementiert im genehmigten Arbeitskontext. Codex bewertet anschließend unabhängig den resultierenden Änderungsstand. Fehlende Agentenläufe dürfen nicht als durchgeführt erscheinen.

**A-03 Wiederaufnahme:** Nach Abbruch/Neustart wird der letzte konsistente Zustand rekonstruiert. Vor erneuter Ausführung potenziell nicht idempotenter Aktionen ist deren Ergebnis festzustellen oder eine Freigabe einzuholen.

**A-04 Freigabegrenzen:** Architektur-, Scope- und sicherheitsrelevante Änderungen sind nach Risikoregeln zu behandeln. Die finale Integration benötigt immer die ausdrücklich auf Änderungsstand und Zielbranch bezogene PO-Freigabe.

**A-05 Review und Tests:** Pflichtprüfungen liefern Belege mit Bezug zum geprüften Commit/Arbeitsstand. Ein negatives oder fehlendes Pflichtresultat verhindert die Integration, sofern keine explizit zulässige und dokumentierte PO-Ausnahme vorliegt.

**A-06 Git-Isolation:** Ein Auftrag bearbeitet einen eigenen Branch/Worktree. Bereits vorhandene ungesicherte Nutzeränderungen dürfen nicht überschrieben werden. Ein Worktree allein ist keine Sicherheits-Sandbox.

**A-07 Freigabewarteschlange:** Eine Freigabe blockiert nur die abhängigen Schritte. Ist kein weiterer zulässiger Schritt im aktuellen Auftrag möglich, wird dessen Zustand gesichert und der aktive Ausführungsplatz für den nächsten Auftrag frei.

**A-08 Berechtigungen:** Fehlt ein technisch wirksamer Mechanismus für die notwendige Beschränkung, darf die Aktion nicht ungeschützt ausgeführt werden. Secrets dürfen nicht unkontrolliert in Logs oder Agentenausgaben gelangen.

**A-09 Änderungsmanagement:** Nach genehmigter Änderung des Auftrags werden betroffene Planung, Implementierung, Tests, Reviews und Freigaben gezielt ungültig gemacht und wiederholt.

**A-10 Historie:** Die Historie beschreibt beobachtbare Handlungen und ausdrücklich ausgegebene Begründungen; sie behauptet keinen Zugriff auf interne Gedankengänge der Modelle.

**A-11 Ressourcen:** Harte Grenzen sind auch bei Modell-Fallback, Retry und Wiederaufnahme einzuhalten. Unbekannte Kontingente dürfen nicht als exakt gemessen dargestellt werden.

**A-12 Integration:** Nach PO-Freigabe werden Zielbranch, Quellstand, Quality Gates und Konflikte erneut geprüft. Bei Abweichung keine stillschweigende Integration.

## 7. Qualitätsanforderungen und Risiken

| ID | Qualitätsanforderung | Nachweis / Status |
|---|---|---|
| N-001 | Integrität und Wiederanlaufsicherheit | Abbruch- und Retry-Szenarien ohne verlorene Freigaben oder doppelte riskante Aktionen; abgeleitet |
| N-002 | Trennung von Implementierung und unabhängiger Prüfung | Review-Nachweis eines getrennten Agentenlaufs; beschlossen |
| N-003 | Technische Zugriffskontrolle | Negativtest verbotener Dateisystem-/Netzwerk-/Werkzeugaktion; beschlossen |
| N-004 | Vertraulichkeit | Redaktions-/Geheimnisprüfung für Logs, UI, Benachrichtigungen; konkretisieren |
| N-005 | Transparenz und Auditierbarkeit | Vollständige, referenzierbare Ereignishistorie; beschlossen |
| N-006 | Anbieterunabhängigkeit der Auftragsverwaltung | Lokaler Auftrag ohne GitHub; beschlossen |
| N-007 | Erweiterbarkeit | Trennung von Orchestrator, Agentenadaptern und optionalen Integrationen; abgeleitet |
| N-008 | Bedienbarkeit | MVP-Grundoperationen über CLI und Dashboard; beschlossen |
| N-009 | Prüfbarkeit | Jedes MVP-Muss-Kriterium besitzt Abnahmebeleg; beschlossen |

**Risiken:** Prompt-Injection durch Repository-Inhalte; Agenten mit zu weitreichenden Shell-Rechten; unkontrollierte API-/Abo-Limits; Änderungen am Zielbranch zwischen Review und Merge; inkonsistente CLI-/Dashboard-Zustände; wiederholte nicht-idempotente Aktionen; unklare Richtlinienhierarchie; wachsende MVP-Komplexität. Gegenmaßnahmen sind die Anforderungen zu Berechtigungen, Versionierung, Quality Gates, Freigaben, Isolation und Persistenz. Quantitative Sicherheits- und Verfügbarkeitsziele sind noch offen.

## 8. Fachliche Datenobjekte und Zustände

**Vorgeschlagene Kernobjekte (noch nicht als Datenmodell beschlossen):** Projekt, Projektregel, Auftrag, Auftragsversion, Akzeptanzkriterium, Abhängigkeit, Plan, Agentenlauf, Modellentscheidung, Worktree/Änderungsstand, Testnachweis, Review-Befund, Freigabeanfrage, PO-Entscheidung, Änderungsantrag, Ressourcenlimit, Ereignis, Integrationsnachweis.

**Vorgeschlagene Zustände:** Entwurf, Klärung, freigegeben/bereit, eingeplant, Planung, Implementierung, Test, Review, Nachbesserung, wartet auf Freigabe, blockiert, pausiert, integrationsbereit, Integration, abgeschlossen, fehlgeschlagen, abgebrochen. Exakte Zustandsmaschine und Übergänge sind offen. „Blockiert“ kann sich auf einen Arbeitsschritt beziehen; „aktiv“ bezeichnet im MVP einen reservierten Ausführungsplatz für einen Auftrag.

## 9. MVP-Abgrenzung und Ausbaustufen

**Beschlossen:** stufenweiser MVP; CLI plus einfache Web-Oberfläche; sequenzielle Ausführung mit Warteschlange; Blockade gibt Ausführungsplatz frei; szenariobasierte Abnahme in Test- und Pilotprojekt. **Noch nicht formal beschlossen:** vollständige Zuordnung jeder Funktion zu einem Release.

### 9.1 Vorgeschlagener verbindlicher MVP-Mindestumfang (zur PO-Freigabe)

| Bereich | MVP-Muss (Vorschlag) | Begründung |
|---|---|---|
| Auftrag | Strukturierte PO-bestätigte Aufträge, Versionierung, Änderungsprüfung | Verbindlicher Umfang |
| Agenten | Echte Codex-/Claude-CLI-Aufrufe, Plan/Implementierung/Test/Review/Korrektur | End-to-End-Nutzen |
| Steuerung | Persistente Ereignisse, Wiederaufnahme, Warteschlange, Freigaben, Eskalation | Betriebsfähigkeit |
| Qualität | Pflicht-Quality-Gates, Review-Belege, szenariobasierte Tests | Nachweisbare Sicherheit |
| Isolation | Git-Branch und Worktree je Auftrag | Schutz des stabilen Arbeitsstands |
| Integration | PO-Gate, Stand-/Konfliktprüfung, automatische Übernahme nach Freigabe | Vollständiger Workflow |
| Bedienung | CLI und schlankes lokales Dashboard mit Status, Start, Pause, Fortsetzen, Abbruch, Freigabe | Beschlossener MVP |
| Sicherheit | Technisch wirksame Mindestberechtigungen, keine ungeschützte Ausführung | Unverzichtbare Grenze |
| Nachweise | Strukturierte Historie und relevante Dokumentationspflege | Nachvollziehbarkeit |
| Ressourcen | Harte Auftragslimits und einfache systemweite Schutzgrenzen | Keine Endlosschleifen |
| Abnahme | Kontrolliertes Testprojekt + realer Pilotauftrag | Q-001/Q-002 |

**Nicht automatisch MVP-Muss:** vollständige Multiprojektverwaltung, parallele Ausführung, umfangreiche Modelloptimierung und adaptive Ergebnisstatistik, sämtliche Benachrichtigungskanäle, vollständiges geführtes Onboarding, umfassende Updateverwaltung, Remote-Worker, vollständige GitHub-Synchronisierung. Architektureignung für spätere Erweiterung bleibt erforderlich.

### 9.2 Vorgeschlagene Stufen nach dem MVP

- **Ausbau A:** erweiterte Modellprofile/Fallback-Analyse, mehrstufige Ressourcenberichte, Benachrichtigungen, Onboarding und umfassendere Dashboard-Funktionen.
- **Ausbau B:** zentrale Multiprojektverwaltung, parallele isolierte Ausführung, Konflikt-/Abhängigkeitsmanagement, optionaler GitHub-Adapter.
- **Ausbau C:** Remote-Worker und kontrollierte Produktupdates mit Zustandsmigration.

Diese Reihenfolge ist eine Planungsempfehlung, keine vom PO bestätigte Release-Reihenfolge.

## 10. MVP-Abnahmekatalog

| ID | Szenario | Erwarteter Nachweis |
|---|---|---|
| T-01 | Vollständiger erfolgreicher Auftrag ohne GitHub | Codex-Plan, Claude-Änderung/Tests, Codex-Review, PO-Gate, Integration |
| T-02 | Implementierung mit Review-Befund | Korrektur und erneutes unabhängiges Review |
| T-03 | Fehlender oder negativer Quality Gate | Keine Integration |
| T-04 | Prozessabbruch während eines Agentenlaufs | Sichere Wiederaufnahme ohne unkontrollierte Doppelaktion |
| T-05 | PO-Freigabe ausstehend | Abhängige Aktion blockiert, Freigabe bleibt gespeichert |
| T-06 | Blockierter DEV-001, wartender DEV-002 | DEV-002 startet, DEV-001 wird später wieder eingeplant |
| T-07 | Laufenden Auftrag ändern | Version, Folgenanalyse, PO-Entscheidung und gezielte Neubewertung |
| T-08 | Wiederholt fehlgeschlagene Korrekturen | Fortschrittsbezogene Eskalation, kein endloser Retry |
| T-09 | Unzulässiger Datei-/Netzwerk-/Toolzugriff | Aktion technisch verweigert und protokolliert |
| T-10 | Ressourcenlimit erreicht | Sicherer Stopp/Blockade, keine verdeckte Überschreitung |
| T-11 | Zielbranch nach Review verändert | Freigabe-/Integrationsstand neu geprüft, kein blinder Merge |
| T-12 | Dokumentation vom Code abweichend | Review-Befund und Korrektur vor Integration |
| T-13 | CLI und Dashboard parallel bedienen | Identische Auftragszustände und Entscheidungen |
| T-14 | Kontrolliertes Testprojekt | Definierte Erfolgs- und Fehlerfälle dokumentiert |
| T-15 | Reales Pilotprojekt | Begrenzter echter Auftrag mit Prüfbelegen und PO-Entscheidung |

**Abnahmebedingung (Vorschlag):** Alle als Muss klassifizierten Szenarien bestehen, kritische Befunde sind geschlossen, verbleibende Risiken ausdrücklich dokumentiert und der PO erteilt die formale Freigabe. Messschwellen für Zeit/Verfügbarkeit/Fehlerquote sind offen.

## 11. Offene Fragen und Entscheidungen vor der Baseline

| ID | Offener Punkt | Priorität | Status |
|---|---|---|---|
| O-01 | Verbindliche MVP-Muss-Liste aus Kapitel 9, inklusive Reihenfolge der Ausbaustufen | Hoch | Offen |
| O-02 | Freigabematrix für Push, PR, Netzwerk, externe Dienste, Dateizugriffe und kritische Befehle | Hoch | Offen |
| O-03 | Technisch durchsetzbare Sandbox-/Berechtigungsmechanismen der eingesetzten CLI-Versionen | Hoch | Offen / Machbarkeit |
| O-04 | Unterstützte Betriebssysteme, CLI-Versionen und Mindestvoraussetzungen | Hoch | Offen |
| O-05 | Exakte Auftragszustände, sichere Haltepunkte, Retry-/Idempotenz- und Abbruchregeln | Hoch | Offen |
| O-06 | Standardlimits für Laufzeit, Versuche, Ressourcen und Eskalationsschwellen | Hoch | Offen |
| O-07 | Vorrang von globalen, projektbezogenen und auftragsbezogenen Richtlinien | Hoch | Offen |
| O-08 | Secrets, Datenaufbewahrung, Datenschutz, Audit-Retention und Zugriffsschutz | Hoch | Offen |
| O-09 | Git-Voraussetzung des MVP und Behandlung von Projekten ohne Git | Hoch | Offen |
| O-10 | Umfang der optionalen GitHub-Synchronisierung, Konfliktverhalten | Mittel | Offen |
| O-11 | Benachrichtigungskanäle, Fristen und Zustellgarantien | Mittel | Offen |
| O-12 | Quantitative Leistungs-, Verfügbarkeits- und Kosten-Zielwerte | Mittel | Offen |
| O-13 | Mehrbenutzerfähigkeit und spätere Rollenmodelle | Mittel | Offen |
| O-14 | Datenformat der Lastenheft-/Auftragsübergabe, Import/Export | Mittel | Offen |
| O-15 | Kriterien für „Fortschritt“, Reviewzyklus-Grenzen und Modellwechsel | Hoch | Offen |
| O-16 | Umgang mit Integrationskonflikten, Wiederherstellung und Zielbranch-Schutz | Hoch | Offen |
| O-17 | Konkrete Auswahl des realen Pilotprojekts und seiner Aufgabe | Mittel | Offen |

**Hinweis zu älteren Unterlagen:** Eine frühere Fassung nannte „maximal drei reguläre Reviewzyklen“. Die neu bestätigte Entscheidung F-023 fordert fortschrittsabhängige Eskalation und konfigurierbare harte Limits. Die Zahl **drei** ist deshalb hier nicht als neue verbindliche Produktgrenze übernommen; O-15 ist zu klären.

## 12. Konsistenz- und Abgrenzungsprüfung (vorläufig)

1. **GitHub-unabhängig ≠ Git-unabhängig.** Die optionale GitHub-Anbindung ist beschlossen; der MVP nutzt Git-Worktrees. Die Unterstützung nicht versionierter Verzeichnisse bleibt offen.
2. **Ein aktiver Auftrag ≠ nur ein gespeicherter Auftrag.** F-028 erlaubt viele wartende/blockierte Aufträge, aber nur einen aktiven Auftrag zur selben Zeit.
3. **Blockade ≠ globaler Stillstand.** F-020 blockiert abhängige Schritte; F-029 erlaubt bei vollständig blockiertem Auftrag einen anderen Auftrag.
4. **Dashboard im MVP ≠ vollständige Verwaltungsplattform im MVP.** F-017 gilt bereits im MVP; F-015 und weitergehende Dashboard-Funktionen können später folgen.
5. **Worktree ≠ Sandbox.** F-018 schützt Git-Arbeitsstände, S-001 schützt gegen unzulässige Prozesse/Datei-/Netzwerkaktionen.
6. **Autonomie ≠ Selbstfreigabe.** F-003/F-019 verlangen weiterhin konkrete PO-Entscheidungen bei kritischen Aktionen und Integration.
7. **Dokumentationspflege ≠ Änderung der Regeln.** F-026 erlaubt Vorschläge und geprüfte Dokumentationsänderungen, aber kein selbstständiges Abschwächen verbindlicher Policies.
8. **Historisches Issue-first ≠ GitHub-Pflicht.** Die kanonische Auftragsverwaltung bleibt lokal; GitHub-Issues sind optionale Abbildungen.
9. **ChatGPT-Begleitung ≠ Laufzeitabhängigkeit.** F-005 beschreibt die fachliche Schnittstelle; der Orchestrator muss autonom und persistent arbeiten.
10. **Älterer Entwurf vs. aktuelle Interviews:** Die Kennungen des Entwurfs vom 13.10.2026 wurden teilweise anders verwendet. Die hier dokumentierten Interview-IDs sind maßgeblich; vor Baseline ist eine ID-Mapping-Tabelle bei Bedarf zu ergänzen.

## 13. Technische Randbedingungen, ohne Architekturfestlegung

**Festgelegt:** lokale Ausführung zuerst; Codex CLI und Claude Code CLI; gemeinsamer persistenter Zustand; Git-Worktrees für Entwicklungsaufträge; CLI und lokale Web-Oberfläche; optionaler GitHub-Adapter; technische Durchsetzung von Berechtigungen. **Nicht festgelegt:** Programmiersprache, Datenbank, Framework, konkrete Event-Engine, IPC-Protokoll, Secrets-Speicher, Betriebssystemmatrix, Hosting, Containerpflicht oder CI-Anbieter. Diese Entscheidungen gehören in das Pflichtenheft bzw. die technische Architektur, soweit sie nicht für die fachliche Baseline sicherheitskritisch sind.

## 14. Prüf- und Freigabeverfahren

1. Fachliche Konsolidierung und Abgleich aller bestätigten Entscheidungen.
2. Prüfung auf Lücken, Widersprüche, Testbarkeit und MVP-Priorisierung.
3. PO-Entscheidungen zu den hoch priorisierten offenen Punkten.
4. **Tatsächlich ausgeführtes unabhängiges Codex-Review** der konsolidierten Fassung mit dokumentierten Befunden. Noch nicht durchgeführt.
5. Einarbeitung bzw. dokumentierte PO-Entscheidung zu Review-Befunden.
6. Formale PO-Freigabe der eindeutig versionierten Baseline.
7. Erst anschließend verbindliche technische Konzeption und Umsetzung gegen die Baseline.

**Aktueller Stand:** fachlicher Entwurf erstellt; keine unabhängige Codex-Prüfung nachgewiesen; keine PO-Freigabe; keine Baseline gesetzt. Die hier dokumentierten Anforderungen sind nicht als bereits implementiert zu verstehen.

## 15. Änderungsverlauf

| Version | Datum | Änderung | Freigabe |
|---|---|---|---|
| 1.0-Entwurf | 14.10.2026 | Zusammenführung des vorhandenen Entwurfs und der nachfolgenden bestätigten Interviewentscheidungen bis Q-002/P-001; MVP-Abgrenzung, Szenarien und offene Fragen überarbeitet | Ausstehend |

---

**Ende des Lastenheft-Entwurfs 1.0.**
