# Logmira

Logmira has been created as a helpful download of Microsoft Windows Domain Group Policy Object settings. This GPO Backup inclues our recommended windows logging settings for all supported versions of MS Windows Server. As opposed to following a list and manualy modifying 100 or so settings, it's way easier to just import it from a backup.

<b> NOTE:</b> Applying these settings are NOT recommended for devices with HDDs. The iop limits on spinning disks can cause issues with the delay of logs when they are a high volume.

<h2>Logmira - Full Verbosity Files</h2>
<ul>
<li>Logmira-FV.zip contains the full GPO backup of only the recommended windows logging settings</li>
<li>gporeport.xml is also included inside the zip, but gives an overview of the settings within the backup</li>
</ul>

<h2>Logmira - Reduced Verbosity Files</h2>
<ul>
<li>Logmira-RV.zip contains the full GPO backup of only the recommended windows logging settings, MINUS process creation and Audit Filtering Platform Connections</li>
<li>gporeport.xml is also included inside the zip, but gives an overview of the settings within the backup</li>
</ul>

<h2>Exporting a GPO </h2>
(what we've done to create the zip files above, and what should be done for GPO Backups)
<ol>
<li>To begin the export process, open up the group policy management console, navigate to the proper domain, expand group policy objects and select the group policy object that you'd like to export.</li>
<li>Right-click and select Back Up.</li>
<li>Select the location the backup will be exported to, and the description. Then click Back Up.</li>
<li>The files are then exported to the location selected, click OK.</li>
</ol>
<h2>Importing a GPO</h2>
<ol>
<li>After the file on the local DC, navigate to the same place in group policy management (the proper domain and expand group policy objects).</li>

<b>NOTE: </b>Do not import settings on an existing GPO unless you want all settings overwritten by the import

<li>Create a NEW GPO by right-clicking on Group Policy Objects > New. </li>
<li>Give the new GPO a name (for example: Logging Settings)</li>
<li>Right-click on the new GPO>"Import Settings"</li>
<li>Next > Next > Select the location where the backup was saved if it is not selected already > Next</li>
<li>Select the "Logging Template" Backed up GPO > Next > Next > Finish</li>
</ol>
You should now have a GPO created that you can link to any OU in your domain to apply the correct logging settings.


