---
title: "[Jenkins] Change Assembly"
categories:
  - Jenkins
tags:
  - Assembly
use_math: true
---
프로그램의 Build Number를 바꾸기 위해 Change Assembly Version이라는 Plugin을 사용했었습니다.  
하지만 아래 그림처럼 Jenkins에서 설정한 Parameter를 적용할 수가 없어서 다른 방법을 찾다가 PowerShell을 이용해서 적용하는 방법을 찾았습니다.  

[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgVk1MtoLfzM5GawzMBerPyOvqEk0E9Snx34BpPWMClkt9VAsH8rkaQHHbWkxdbuOiwvruMs8QPyLOqW94tSDIAArvfR8P9iO91cD1ZlJRoC69buMTQwIzGVb-ayXLB0KWaVBTGTp54paK2kLhqt5pnc1o8x9zsDPRisLScSB-Jwt7bqBKR09v5CT5qeBU/s600/Pasted%20image%2020240411143510.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgVk1MtoLfzM5GawzMBerPyOvqEk0E9Snx34BpPWMClkt9VAsH8rkaQHHbWkxdbuOiwvruMs8QPyLOqW94tSDIAArvfR8P9iO91cD1ZlJRoC69buMTQwIzGVb-ayXLB0KWaVBTGTp54paK2kLhqt5pnc1o8x9zsDPRisLScSB-Jwt7bqBKR09v5CT5qeBU/s1256/Pasted%20image%2020240411143510.png)

아래 그림처럼 Parameter를 사용하려고 했지만 적용되지 않았습니다.  
[![](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhn8my59AK7a25VxpUWEsAiFmGhaByn7NrHW016-WuHci74lBPL4m1mzmlYRqxe53UX_YI2ND3r7m7g6caivHEbmTmn22h1GWNtdxAWwp9Kvav7Q4qIuoUxlwkveogvLCc8YRKmN_w0tv1ASJNMNJjb5f6kC1a2L2TxyQVc9arKF7W5NdkFql9cTVo9Fgk/s600/Pasted%20image%2020240411143606.png)](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhn8my59AK7a25VxpUWEsAiFmGhaByn7NrHW016-WuHci74lBPL4m1mzmlYRqxe53UX_YI2ND3r7m7g6caivHEbmTmn22h1GWNtdxAWwp9Kvav7Q4qIuoUxlwkveogvLCc8YRKmN_w0tv1ASJNMNJjb5f6kC1a2L2TxyQVc9arKF7W5NdkFql9cTVo9Fgk/s1257/Pasted%20image%2020240411143606.png)

아래 PowerShell 코드를 사용하면 매개 변수로 설정한 Parameter를 적용할 수 있습니다.  
COMPANY라는 Parameter는 PowerShell에서 $env:COMPANY로 접근할 수 있습니다.

```powershell
# Get the AssemblyInfo.cs
$assemblyInfo = Get-Content -Path .\$env:COMPANY\Properties\AssemblyInfo.cs
 
# Replace last digit of AssemblyVersion
$assemblyInfo = $assemblyInfo -replace 
    "^\[assembly: AssemblyVersion\(`"([0-9]+)\.([0-9]+)\.([0-9]+)\.[0-9]+`"\)]", 
    ('[assembly: AssemblyVersion("$1.$2.$3.' + $env:BUILD_NUMBER + '")]')
    Write-Host  ($assemblyInfo -match '^\[assembly: AssemblyVersion')
        
# Replace last digit of AssemblyFileVersion
$assemblyInfo = $assemblyInfo -replace 
    "^\[assembly: AssemblyFileVersion\(`"([0-9]+)\.([0-9]+)\.([0-9]+)\.[0-9]+`"\)]", 
    ('[assembly: AssemblyFileVersion("$1.$2.$3.' + $env:BUILD_NUMBER + '")]')
    Write-Host  ($assemblyInfo -match '^\[assembly: AssemblyFileVersion')
        
$assemblyInfo | Set-Content -Path .\$env:COMPANY\Properties\AssemblyInfo.cs -Encoding UTF8
```