## Advanced Microsoft Commandline Logging via GPO

For advanced Microsoft commandline and powershell module logging, make the following changes to group policy.

---
* `Computer Configuration > Policies > Windows Settings > Security Settings > Advanced Audit Configuration > Detailed Tracking > Audit Process Creation > Enable`
* `Computer Configuration > Policies > Administrative Templates > System > Audit Process Creation > Include command line in process creation events > Enable`
* `User Configuration > Policies > Administrative Templates > Windows Components > Windows Powershell > Enable and set module names to *`

If you also want to audit WMIC activity, you must run the following command on hosts that you want to collect WMIC tracing logs from.  This must be run in an elevated prompt.
```
Wevtutil.exe sl Microsoft-Windows-WMI-Activity/Trace /e:true /q:true
```
