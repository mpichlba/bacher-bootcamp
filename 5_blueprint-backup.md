# Backup mit Blueprints
### Blueprint in Kasten K10 hinzufügen:
```
kubectl --namespace kasten-io apply -f \
    https://raw.githubusercontent.com/kanisterio/kanister/0.92.0/examples/postgresql/blueprint-v2/postgres-blueprint.yaml
```
### Annotation der Applikation hinzufügen
```
kubectl --namespace postgresql annotate statefulset/postgres-postgresql \
    kanister.kasten.io/blueprint=postgres-bp
```
### Anpassen der Backup Policy
- Dashboard -> Policies
- Policy "postgresql-backup" suchen und editieren ("edit")
- Location profile unter "Location Profile for Kanister Actions" auswählen
- "Edit Policy"

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
