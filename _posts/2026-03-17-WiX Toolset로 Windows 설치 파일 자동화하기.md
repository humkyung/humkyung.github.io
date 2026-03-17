---
title: WiX Toolset로 Windows 설치 파일 자동화하기
date: 2026-03-17
categories:
  - wxs
  - Jenkins
tags:
  - wxs
  - Jenkins
img_path: /assets/images/
---
## NSIS에서 WiX로

예전에 프로그램을 만들고 나면 설치 파일을 배포해야 했는데, 처음에는 Winamp로 유명한 Nullsoft에서 만든 **NSIS**를 사용했습니다. InstallShield라는 강력한 툴도 있었지만 상용이라 freeware인 NSIS를 선택했고, 구글링과 블로그를 뒤져가며 열심히 공부했던 기억이 납니다.

이후 마이크로소프트에서 만든 **WiX Toolset**을 알게 되면서 NSIS 대신 WiX를 사용하게 되었습니다.

---

### WiX Toolset 기본 구조

WiX는 XML 기반(.wxs)으로 설치 파일을 구성합니다. 주요 도구는 세 가지입니다.

| 도구           | 역할                 |
| ------------ | ------------------ |
| `heat.exe`   | 설치할 파일 목록 자동 생성    |
| `candle.exe` | .wxs → .wixobj 컴파일 |
| `light.exe`  | .wixobj → .msi 링크  |

`heat.exe`로 설치 대상 디렉토리를 스캔하면 파일 목록이 담긴 .wxs 파일이 자동으로 생성됩니다.
```bash
SET yyyymmdd=%DATE:~0,4%-%DATE:~5,2%-%DATE:~8,2%
SET hhmmss=%TIME:~0,2%-%TIME:~3,2%-%TIME:~6,2%
SET hhmmss=%hhmmss: =0%

SET HEAT="C:\Program Files (x86)\WiX Toolset v3.11\bin\heat.exe"
SET CANDLE="C:\Program Files (x86)\WiX Toolset v3.11\bin\candle.exe"
SET LIGHT="C:\Program Files (x86)\WiX Toolset v3.11\bin\light.exe"

%HEAT% dir SourceFolder -dr INSTALLFOLDER -cg ProductName -g1 -gg -sf -srd -scom -sreg -t HeatTransform.xslt -out ".\fragments.wxs"
```

![Pasted image 20260317160023](/assets/images/Pasted image 20260317160023.png)

생성된 파일에는 설치 대상 파일 목록만 포함되어 있기 때문에, 설치 화면(배너, 설치 경로 선택, 언인스톨 등)은 별도로 직접 작성해야 합니다.
![Pasted image 20260317160820](/assets/images/Pasted image 20260317160820.png)

그렇게 만들어진 .wxs 파일은 다음 명령으로 빌드합니다.
```bash
Del Setup\*.wixpdb
Del Setup\*.wixobj
Del Setup\*.msi

%CANDLE% ".\Sample.wxs" -out .\Setup\

IF %ERRORLEVEL% NEQ 0 goto :ERROR

%LIGHT% -out ".\Setup\Sample.msi" ".\Setup\Sample.wixobj" -ext WixUIExtension -ext WixUtilExtension
```

---
### 파일 목록과 UI 분리하기

한동안 잘 사용했지만 문제가 생겼습니다. 프로그램이 업데이트될 때마다 변경된 파일을 .wxs 파일에 **수작업으로** 추가해야 했습니다. 파일 한두 개라면 괜찮지만, 파일이 많아질수록 이 작업은 꽤 번거롭고 실수가 생기기도 했습니다.

해결책은 간단합니다. **파일 목록과 UI를 분리**하는 것입니다.

- **뼈대 .wxs**: 설치 화면, 단축키, 디렉토리 구조 등 고정된 부분
- **heat 생성 .wxs**: 설치 대상 파일 목록 (자동 생성)

뼈대 파일은 아래와 같은 구조로 작성합니다. heat가 생성한 `InstallFiles` 컴포넌트 그룹을 참조하는 것이 핵심입니다.
```XML
<?xml version="1.0" encoding="UTF-8"?>
<Wix xmlns="http://schemas.microsoft.com/wix/2006/wi">

  <?define SourceDir=".\Publish\Client"?>

  <Product Id="*" Name="ProductName" Language="1033" Version="{VERSION}"
           Manufacturer="Company"
           UpgradeCode="cda2aef0-4a20-4642-9f89-af01feafc8e7">

    <Package Platform="x64" InstallerVersion="200" Compressed="yes" InstallScope="perMachine"/>

    <MajorUpgrade Schedule="afterInstallInitialize"
                  DowngradeErrorMessage="A newer version of [ProductName] is already installed."
                  AllowSameVersionUpgrades="yes"/>

    <MediaTemplate EmbedCab="yes"/>

    <Feature Id="ProductFeature" Title="ProductName" Level="1">

        <!-- heat 자동 생성 파일 -->
        <ComponentGroupRef Id="InstallFiles"/>

        <!-- Desktop shortcut component -->
        <ComponentRef Id="DesktopShortcut"/>

    </Feature>

    <!-- 설치 위치 -->
    <Property Id="WIXUI_INSTALLDIR" Value="InstallFolder"/>
    <UIRef Id="WixUI_InstallDir"/>

    <!-- 설치 완료 후 실행 -->
    <UI>
        <Publish Dialog="ExitDialog"
                 Control="Finish"
                 Event="DoAction"
                 Value="LaunchApplication">
            WIXUI_EXITDIALOGOPTIONALCHECKBOX = 1 and NOT Installed
        </Publish>
    </UI>

    <Property Id="WIXUI_EXITDIALOGOPTIONALCHECKBOXTEXT" Value="Launch ProductName"/>
    <Property Id="WixShellExecTarget" Value="[InstallFolder]ProductName.exe"/>

    <CustomAction Id="LaunchApplication"
                  BinaryKey="WixCA"
                  DllEntry="WixShellExec"
                  Impersonate="yes"/>

    <Directory Id="TARGETDIR" Name="SourceDir">

        <!-- Desktop shortcut -->
        <Directory Id="DesktopFolder">
            <Component Id="DesktopShortcut" Guid="44D6BF99-8203-4DF8-A7F4-1FDC717A6B8C">

                <RegistryValue
                    Root="HKCU"
                    Key="Software\Company\ProductName"
                    Name="installed"
                    Type="integer"
                    Value="1"
                    KeyPath="yes"/>

                <Shortcut
                    Id="DesktopShortcutLink"
                    Name="ProductName"
                    Description="Product Description"
                    Target="[InstallFolder]ProductName.exe"
                    WorkingDirectory="InstallFolder"/>

                <RemoveFolder Id="RemoveDesktopFolder" On="uninstall"/>

            </Component>
        </Directory>

        <Directory Id="ProgramFiles64Folder">
            <Directory Id="Company" Name="Company">
                <!-- heat와 동일 -->
                <Directory Id="InstallFolder" Name="ProductName"/>
            </Directory>
        </Directory>
    </Directory>
  </Product>
</Wix>
```

저희는 Jenkins의 PowerShell 스크립트에서 빌드 시마다 파일 목록을 자동으로 생성하도록 구성했습니다.
```PowerShell
Write-Host "=== Generate InstallFiles.wxs with heat ==="

$outFile = ".\InstallModule\InstallFiles.wxs"

if (Test-Path $outFile) {
    Remove-Item $outFile -Force
}

& %HEAT% dir ".\Publish\Client" `
  -cg InstallFiles `
  -dr InstallFolder `
  -var var.SourceDir `
  -srd `
  -sreg `
  -sfrag `
  -gg `
  -t transform.xslt `
  -out $outFile
```

---
### 정리

이렇게 뼈대 파일과 파일 목록을 분리해두면, 이후 설치 대상 파일이 아무리 바뀌어도 **별도의 수정 없이** 빌드 파이프라인이 알아서 최신 목록을 반영한 설치 파일을 만들어줍니다. 단순해 보이지만 반복적인 수작업을 없애는 것만으로도 실수를 줄이고 유지보수가 훨씬 편해집니다.