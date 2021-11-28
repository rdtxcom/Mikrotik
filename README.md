# Mikrotik

Scripts para Mikrotik:
Auto generación de backups y export y envío a servidor ftp:

/system backup save name= ("BACKUP"."-".[/ system identity get name]."-". \
[: pick [/ system clock get date] 4 6].[: pick [/ system clock get date] 0 3].[: pick [/ system clock get date] 7 11]);
/ export file=("BACKUP"."-".[/ system identity get name]."-". \
[: pick [/ system clock get date] 4 6]. [: pick [/ system clock get date] 0 3]. [: pick [/ system clock get date] 7 11]);
: global backupname ("BACKUP"."-".[/ system identity get name]."-". \
[: pick [/ system clock get date] 4 6].[: pick [/ system clock get date] 0 3].[: pick [/ system clock get date] 7 11]. ".backup");
/ tool fetch address=IP.SERVER.FTP mode=ftp user=USER.FTP password=PASWOORD.FTP src-path=$backupname dst-path="DIR.FTP/$backupname" upload=yes;
: global backupname ("BACKUP"."-".[/ system identity get name]."-". \
[: pick [/ system clock get date] 4 6].[: pick [/ system clock get date] 0 3].[: pick [/ system clock get date] 7 11]. ".rsc");
/ tool fetch address=IP.SERVER.FTP mode=ftp user=USER.FTP password=PASWOORD.FTP src-path=$backupname dst-path="DIR.FTP/$backupname" upload=yes;
/file remove  ("BACKUP"."-".[/ system identity get name]."-". \
[: pick [/ system clock get date] 4 6].[: pick [/ system clock get date] 0 3].[: pick [/ system clock get date] 7 11]. ".backup")
/file remove  ("BACKUP"."-".[/ system identity get name]."-". \
[: pick [/ system clock get date] 4 6].[: pick [/ system clock get date] 0 3].[: pick [/ system clock get date] 7 11]. ".rsc")


