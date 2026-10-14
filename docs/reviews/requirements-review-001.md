## Ergebnis

Das Lastenheft ist als fachlicher Entwurf umfangreich und transparent, aber noch nicht baselinefähig. Eine PO-Freigabe sollte zum geprüften Stand nicht erteilt werden.

Geprüfter Git-Commit:

14828cb9f05b220d3b10e4bd34ed43d81b28e1c8

Arbeitsbaum: sauber. Es wurden keine Dateien verändert und keine Implementierungstätigkeiten ausgeführt.

## Einordnung des Dokumentstands

- Als fachlich beschlossen/interviewbestätigt bezeichnet: Ziele, Rollen, Sollprozess sowie Anforderungen R-001 bis R-003, F-002 bis F-029, S-001 und Q-001/Q-002.
- Als Vorschlag gekennzeichnet: P-001, der MVP-Mindestumfang in Kapitel 9.1, Ausbaustufen, Datenobjekte, Zustände und Abnahmebedingung.
- Offen: O-01 bis O-17, insbesondere MVP-Grenze, Berechtigungen, CLI-/OS-Voraussetzungen, Zustandsmaschine, Retry-Regeln, Datenaufbewahrung und Integrationsverhalten.
- „Beschlossen“ bedeutet laut Dokument selbst nur interviewbestätigt, nicht PO-freigegeben oder implementiert.

## Befunde

### BLOCKER

B-001 — Keine formale Baseline-Freigabe

- Referenz: lastenheft-v1.0.md:3-8, :251-261, :265-267
- Problem: Das Dokument ist ausdrücklich ein Entwurf; PO-Freigabe und Baseline sind ausstehend. Eine Approval-Entscheidung mit Approver, Datum und unveränderlicher Revision fehlt.
- Auswirkung: Nach dem Workflow sind RG-04 und RG-08 nicht erfüllt. Das Dokument darf nicht als verbindliche Implementierungsgrundlage verwendet werden.
- Empfehlung: Offene Befunde und Entscheidungen bearbeiten, anschließend die exakte Revision durch den PO freigeben und die Freigabe separat dokumentieren.

B-002 — Sicherheits- und Betriebsgrenzen sind für ein lokal ausführendes Agentensystem nicht entscheidungsreif

- Referenz: :104-108, :126, :138-150, :214-222
- Problem: Technisch durchsetzbare Berechtigungen, Sandbox-Mechanismen, Richtlinienhierarchie, Secrets, Datenschutz, Audit-Aufbewahrung und Zugriffsschutz sind weiterhin offen.
- Auswirkung: Die zentrale Sicherheitsanforderung S-001 ist nicht belastbar abnehmbar. Ein sicherer MVP-Start kann nicht nachgewiesen werden.
- Empfehlung: O-02, O-03, O-07 und O-08 vor der Baseline mit verbindlichen Negativkriterien, erlaubten Aktionen, Schutzmechanismen, Secret-Regeln und Aufbewahrungsregeln entscheiden.

B-003 — MVP-Umfang ist nicht verbindlich festgelegt

- Referenz: :59-62, :94-100, :158-186, :214
- Problem: Beschlossene MVP-Aussagen, vorgeschlagener Mindestumfang und spätere Funktionen sind nicht in einer einzigen verbindlichen Muss-/Soll-/Kann-/Nicht-Ziel-Liste konsolidiert.
- Auswirkung: Unklarer Lieferumfang, nicht belastbare Aufwandsschätzung und keine eindeutige Abnahmebasis.
- Empfehlung: O-01 entscheiden und jede Anforderung eindeutig einem Release sowie einer Priorität zuordnen.

### HIGH

H-001 — Fehlende belastbare Quellen- und Entscheidungsrückverfolgbarkeit

- Referenz: :5-6, :51-53, :57-108, :267
- Problem: Als Herkunft werden nur „Anforderungsinterview“, frühere Gespräche und ein älterer Entwurf genannt. Einzelne Anforderungen haben keine konkrete Quelle, Entscheidung, Datum oder Änderungsbegründung.
- Auswirkung: Anforderungen können nicht zuverlässig gegen Ursprung und Stakeholderentscheidung geprüft werden; Änderungen sind schwer rückverfolgbar.
- Empfehlung: Für jede Anforderung Quelle, Entscheidungsdatum, Entscheider, Status und Abhängigkeiten dokumentieren. Die angekündigte ID-Mapping-Tabelle vor der Baseline ergänzen.

H-002 — Viele Akzeptanzkriterien sind nicht hinreichend testbar

- Referenz: :18-20, :68-108, :112-148, :190-208
- Problem: Begriffe wie „weitgehend autonom“, „sicher“, „risikobasiert“, „geeignet“, „relevante Dokumentation“, „keine unkontrollierte Doppelaktion“ und „vollständig“ sind nicht operationalisiert.
- Auswirkung: Unterschiedliche Implementierungen und Reviewer können zu unterschiedlichen Ergebnissen kommen; Bestehen oder Scheitern ist nicht objektiv feststellbar.
- Empfehlung: Pro Muss-Anforderung Vorbedingungen, auslösende Aktion, erwarteten Zustand, Fehlverhalten, Nachweisformat und gegebenenfalls messbare Schwellen definieren.

H-003 — Zustands-, Retry- und Wiederaufnahmeverhalten ist noch offen

- Referenz: :68, :82-84, :116, :124, :152-156, :218-220, :228
- Problem: Die Anforderungen verlangen Persistenz, Wiederaufnahme, Retry und Eskalation, während Zustandsmaschine, sichere Haltepunkte, Idempotenz, Retry-Grenzen und Fortschrittskriterien offen bleiben.
- Auswirkung: Besonders bei nicht idempotenten Agentenaktionen besteht ein erhebliches Risiko für Doppelaktionen, verlorene Freigaben oder unklare Blockaden.
- Empfehlung: Zustände, erlaubte Übergänge, Wiederanlaufpunkte, Retry-/Abbruchregeln, Eskalationsgrenzen und Zustandskonsistenz als verbindliche Akzeptanzkriterien festlegen.

H-004 — Agenten- und Laufzeitvoraussetzungen sind nicht ausreichend spezifiziert

- Referenz: :30-35, :71-78, :167, :216-217, :247-249
- Problem: Die Nutzung echter Codex- und Claude-CLI-Aufrufe ist vorgesehen, aber Versionen, unterstützte Betriebssysteme, Authentisierung, Exit-/Fehlerverhalten, Modell-Pinning und Mindestumgebung sind offen.
- Auswirkung: Der geforderte End-to-End-MVP ist ohne diese Entscheidungen nicht reproduzierbar abnehmbar.
- Empfehlung: O-03 und O-04 vor der Baseline klären und den minimal unterstützten Ausführungsrahmen festlegen.

H-005 — Integration nach Freigabe ist fachlich noch nicht ausreichend definiert

- Referenz: :47-49, :95-96, :118, :134, :171, :202, :229
- Problem: Automatische Integration wird gefordert, während Konfliktverhalten, Wiederherstellung, Zielbranch-Schutz und Revalidierung offen sind.
- Auswirkung: Die kritischste externe Zustandsänderung des Workflows ist nicht eindeutig abnehmbar.
- Empfehlung: O-16 mit verbindlichen Regeln für Zielbranch-Drift, Konflikte, Rollback/Wiederherstellung und Freigabeinvalidierung entscheiden.

H-006 — PO- und Stakeholder-Verantwortung ist nicht ausreichend konkretisiert

- Referenz: :5, :24-35; Workflow 01-requirements-baseline.md:18-24
- Problem: Der PO ist nur als „Projektverantwortlicher“ bezeichnet; weitere fachliche Rollen und Rechte sind offen.
- Auswirkung: Freigabe, Ausnahmeentscheidungen und Abnahme sind organisatorisch nicht eindeutig zuordenbar.
- Empfehlung: PO, Stellvertretung, betroffene Stakeholder und ihre Entscheidungsrechte vor der Baseline namentlich bzw. rollenbezogen festlegen.

### MEDIUM

M-001 — Keine vollständige Anforderungs-zu-Abnahmekriterium-Matrix

- Referenz: :57-108, :110-134, :188-208
- Problem: Es gibt Kernnachweise und Testszenarien, aber keine eindeutige Zuordnung jeder Muss-Anforderung zu mindestens einem konkreten Test bzw. Nachweis.
- Auswirkung: Lücken in der Abdeckung können unbemerkt bleiben.
- Empfehlung: Traceability-Matrix Anforderung → Akzeptanzkriterium → Testszenario → Evidenz ergänzen.

M-002 — Begriffe und Ebenen sind teilweise mehrdeutig

- Referenz: :35, :46, :68-84, :124, :156, :208
- Problem: „Auftrag“, „Schritt“, „aktiv“, „blockiert“, „kritisch“, „risikoarm“ und „unabhängig“ werden nicht präzise definiert.
- Auswirkung: Uneinheitliche Zustands- und Berechtigungsentscheidungen.
- Empfehlung: Ein verbindliches Glossar mit Definitionen und Abgrenzungen ergänzen.

M-003 — Nichtfunktionale Qualitätsziele fehlen

- Referenz: :143, :150, :208, :225
- Problem: Verfügbarkeit, Laufzeit, Kosten, Fehlerquote, Wiederanlaufdauer und Aufbewahrungsfristen sind offen.
- Auswirkung: Die Anforderungen N-001, N-004, N-005 und N-009 bleiben nur qualitativ prüfbar.
- Empfehlung: Für den MVP mindestens begründete Zielwerte oder ausdrücklich dokumentierte Nicht-Ziele festlegen.

M-004 — Daten- und Lebenszyklusregeln sind nur vorgeschlagen

- Referenz: :152-156, :221, :227
- Problem: Kernobjekte und Zustände sind vorgeschlagen; Eigentum, Versionierung, Aufbewahrung, Löschung, Export und Datenschutzbezug fehlen.
- Auswirkung: Persistenz und Auditierbarkeit können unterschiedlich interpretiert werden.
- Empfehlung: Fachliches Datenmodell, Lebenszyklen und Datenhaltungsregeln mindestens für MVP-Objekte beschreiben.

M-005 — Dashboard- und Benachrichtigungsumfang bleibt unpräzise

- Referenz: :90-94, :172, :223-224
- Problem: Bedienoperationen, Fehlerdarstellung, Rollenprüfung, Benachrichtigungskanäle und Zustellgarantien sind nicht vollständig definiert.
- Auswirkung: F-013, F-014 und F-017 sind nur eingeschränkt abnehmbar.
- Empfehlung: MVP-UI-Operationen und Mindestverhalten bei Fehlern, Parallelbedienung und Benachrichtigungen festlegen.

### LOW

L-001 — Revisionsidentifikation ist nicht im Dokument selbst unveränderlich verankert

- Referenz: :3, :263-267
- Problem: Version und Datum sind vorhanden, der geprüfte Git-SHA jedoch nicht.
- Auswirkung: Eine spätere Approval-Dokumentation könnte versehentlich eine andere Datei gleichen Versionsstands referenzieren.
- Empfehlung: Git-SHA oder eine andere immutable Revision in Review- und Freigabenachweis aufnehmen.

L-002 — Änderungsverlauf beschreibt keine fachlichen Einzelentscheidungen

- Referenz: :265-267
- Problem: Der Änderungsverlauf nennt nur eine zusammenfassende Änderung.
- Auswirkung: Es ist nicht ersichtlich, welche Anforderungen seit dem Entwurf vom 13.10.2026 geändert wurden.
- Empfehlung: Wesentliche Änderungen und deren Entscheidungshintergrund pro Revision dokumentieren.

## Stärken

- Der Entwurfsstatus und die fehlende PO-Freigabe werden ausdrücklich und korrekt offengelegt.
- Bestätigte Inhalte, Vorschläge und offene Fragen werden grundsätzlich unterschieden.
- GitHub wird sinnvoll von Git getrennt; die lokale Nutzung ist klar beschrieben.
- Sicherheitsrisiken, Prompt-Injection, Secret-Schutz, Branch-Drift und nicht-idempotente Aktionen werden erkannt.
- Der Sollprozess deckt Auftrag, Planung, Implementierung, Review, Freigabe, Integration und Wiederaufnahme ab.
- Die Abnahmeszenarien T-01 bis T-15 bilden wesentliche Erfolgs-, Fehler-, Sicherheits- und Wiederanlauffälle ab.
- Das Dokument vermeidet eine vorzeitige Festlegung auf Programmiersprache, Datenbank oder Framework.

## Besonders fehlende Akzeptanzkriterien

Vor einer Baseline sollten mindestens konkrete Kriterien ergänzt werden für:

- technische Verweigerung unzulässiger Datei-, Shell-, Netzwerk- und Toolaktionen;
- Verhalten bei fehlender oder negativer Prüfung;
- exakte Zustandsübergänge und Wiederaufnahme nach Prozessabbruch;
- Retry-Grenzen, Idempotenz und Eskalation;
- Zielbranch-Änderung und Integrationskonflikte;
- Secret-Redaktion, Datenaufbewahrung und Audit-Zugriff;
- CLI-/Dashboard-Konsistenz;
- Mindestumgebung und reproduzierbare CLI-Ausführung;
- verbindliche MVP-Mussliste und deren Testabdeckung.

## Entscheidungen vor Baseline-Freigabe

Prioritär erforderlich sind O-01 bis O-09, O-15 und O-16. O-10 bis O-14 und O-17 können je nach PO-Entscheidung für die Baseline nachgelagert werden, dürfen aber nicht stillschweigend als entschieden gelten.

## Baseline-Urteil

Nicht bereit für PO-Freigabe.

Die formale Freigabe ist bereits wegen fehlender PO-Entscheidung und fehlendem Freigabenachweis ausgeschlossen. Zusätzlich blockieren mehrere offene fachliche und sicherheitsrelevante Entscheidungen die eindeutige MVP-Abgrenzung, Implementierbarkeit und Abnahme.