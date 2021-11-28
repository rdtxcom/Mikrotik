# Mikrotik

Scripts para Mikrotik:
Auto generación de backups y export y envío a servidor ftp: Sustituir valores de la variables por los adecuados.

:global serverftp XX.XX.XX.XX;
:global userftp XXXXXXX;
:global passftp XXXXXXXXXXX;
:global dirftp XXXXXXXXX;
:global backupname ("BACKUP"."-".[/ system identity get name]."-".[: pick [/ system clock get date] 4 6].[: pick [/ system clock get date] 0 3].[: pick [/ system clock get date] 7 11]);

/system backup save name= $backupname;
/export file= $backupname;
/tool fetch address=$serverftp mode=ftp user=$userftp password=$passftp src-path=("$backupname".".backup") dst-path=("$dirftp/$backupname".".backup") upload=yes;
/tool fetch address=$serverftp mode=ftp user=$userftp password=$passftp src-path=("$backupname".".rsc") dst-path=("$dirftp/$backupname".".rsc") upload=yes;

/file remove  ("$backupname".".backup");
/file remove  ("$backupname".".rsc");
