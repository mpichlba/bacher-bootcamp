# K10 Konfiguration

### Login auf K10 URL (Ingres)
zb:
- http://kasten.10.2.200.28.nip.io/k10/# 
- Benutzername: kasten
- Kennwort: bacher

### Konfiguration Location Profile
- Settings
  - Locations
  - New Profile
      - Endpoint: https://10.2.235.191:18082
      - S3 access Key: B8DURN8UU0RPF2VIFB50
      - S3 secret: HyaiQ9t+Lo3/Vx7UV4PogDtRt/TcJBn7uteq1QXG
      - Skip certificate chain and hostname verification: true
      - bucket name: bucket01

### Konfiguration K10 DR
- Dashboard -> Settings -> K10 Disaster Recovery
  - "Enable K10 DR"
  - Cloud Location Profile: "s3" auswählen
  - Passphrase: "bacher"
  - "Enable K10 DR" klicken
- Dashboard -> Policies
 - überprüfen, ob die Policy "k10-disaster-recovery-policy" angelegt wurde
 - Policy mit "run once" starten
- Auf das Dashboard zurückkehren und warten bis das Backup abgeschlossen ist
