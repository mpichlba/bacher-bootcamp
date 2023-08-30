# Restore in einen anderen Cluster

### Importing Data der Backup Policy sichern (Quellcluster)
- Dashboard -> Policies -> "postgresql-backup" Policy suchen
- "Show import Details" anklicken
- "Copy to Clipboard" klicken
- kopierten String in z.B. notepad einfügen

### Mit Ziel-K10-Installation verbinden
#### Liste mit K10 Instanzen und Benutzername/Kennwort (kasten/bacher)

URL: http://kasten.xxx.xxx.xxx.xxx.nip.io/k10/# \
URL: http://kasten.xxx.xxx.xxx.xxx.nip.io/k10/# \
URL: http://kasten.xxx.xxx.xxx.xxx.nip.io/k10/# \
URL: http://kasten.xxx.xxx.xxx.xxx.nip.io/k10/# \
URL: http://kasten.xxx.xxx.xxx.xxx.nip.io/k10/# \
URL: http://kasten.xxx.xxx.xxx.xxx.nip.io/k10/# \
URL: http://kasten.xxx.xxx.xxx.xxx.nip.io/k10/# \
URL: http://kasten.xxx.xxx.xxx.xxx.nip.io/k10/# 

### Import Policy anlegen auf dem Ziel-Cluster
- Dashboard -> Policies -> "Create New Policy"
  - Name: "postgresql-import-\<Quell-Student-ID>
  - Action: "Import"
  - "Restore after Import" aktivieren
  - Import Frequency: "On Demand"
  - Config Data for Import: \<aus dem Notepad>
  - "Create Policy"
 
### Import Policy starten
- Import Policy mit "run once" starten
- Auf das Dashboard zurückkehren und warten bis die Import und Restore Actions abgeschlossen sind


