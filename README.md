# Logmira

Files:
- GPOLoggingImport.zip contains the full GPO backup of only the recommended windows logging settings
- gporeport.xml is also included inside the zip, but gives an overview of the settings within the backup

How to apply to your domain:
To make it easier for our customers, Blumira has exported all of our recommended logging settings (found here https://www.blumira.com/how-to-optimize-windows-logging-for-security/).


Exporting a GPO (what we've done to create GPOLoggingImport.zip, and what should be done for GPO Backups)
1. To begin the export process, open up the group policy management console, navigate to the proper domain, expand group policy objects and select the group policy object that you'd like to export.
2. Right-click and select Back Up.
3. Select the location the backup will be exported to, and the description. Then click Back Up.
4. The files are then exported to the location selected, click OK.

Importing a GPO
1. After the file on the local DC, navigate to the same place in group policy management (the proper domain and expand group policy objects).

##NOTE: Do not import settings on an existing GPO unless you want all settings overwritten by the import

2. Create a NEW GPO by right-clicking on Group Policy Objects > New. 
3. Give the new GPO a name (for example: Logging Settings)
4. Right-click on the new GPO>"Import Settings"
5. Next > Next > Select the location where the backup was saved if it is not selected already > Next
6. Select the "Logging Template" Backed up GPO > Next > Next > Finish

You should now have a GPO created that you can link to any OU in your domain to apply the correct logging settings.


