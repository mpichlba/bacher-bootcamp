# Backup Policies # Backup & Restore:

### Erstellen einer Backup Policy
- Dashboard -> Applications
- Applikation "postgresql" suchen
- Create Backup Policy:
  - Backup Frequency auf "On Demand" ändern" - ansonsten NICHTS ändern
  - "Create Policy"

### Backup Policy starten
- `watch kubectl get po -A`
- Backup Policy mit "run once" starten
- Auf das Dashboard zurückkehren und warten Bis das Backup abgeschlossen ist
- den watch-Befehl vom Anfang verfolgen und nach erfolgreichem Backup mit Strg+c abbrechen

### Löschen der Applikation
- `kubectl delete ns postgresql`

### Wiederherhstellung der Applikation
- `watch kubectl get po -A`
- Dashboard -> Applications
- "Filter by Status" -> "Removed"
- auf "Restore" klicken
- Restorepoint auswählen
- "Restore" ausführen
- Auf das Dashboard zurückkehren und warten bis der Restore abgeschlossen ist
- den watch-Befehl vom Anfang verfolgen und nach erfolgreichem Restore mit Strg+c abbrechen

