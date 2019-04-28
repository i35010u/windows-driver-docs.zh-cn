---
title: 使用扩展 INF 文件
description: 从 Windows 10 开始，你可以扩展驱动程序程序包 INF 文件的功能通过提供一个额外的 INF 文件称为扩展 INF。
ms.assetid: 124C4E58-7F06-46F5-B530-29A03FA75C0A
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: aecaba727d928106b0a1dfc642b01f61e59485ec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339485"
---
# <a name="using-an-extension-inf-file"></a>使用扩展 INF 文件

在 Windows 10 之前 Windows 选择单个驱动程序包以安装适用于给定的设备。  这会导致大型、 复杂的驱动程序包包含代码的所有方案和配置，并且每个次要更新所需对整个驱动程序包的更新。  从 Windows 10 开始，可以拆分成多个组件，可以独立处理每个 INF 功能。  若要将驱动程序扩展包 INF 文件的功能，提供单独的驱动程序包中的一个扩展 INF。  INF 扩展：

* 可以提供不同公司，从基本 INF 独立更新。
* 作为基本 INF，看上去相同但可以扩展基 INF 使用自定义或专用化。
* 增强了的值的设备，但不需要工作的基本驱动程序。
* 必须是[通用 INF 文件](../install/using-a-universal-inf-file.md)。

每个设备必须具有一个基 INF 和 （可选） 可以有一个或多个扩展与之关联的 Inf。

您可能需要使用 INF 的扩展的典型方案包括：

* 修改基 INF，例如自定义设备友好名称或修改硬件配置设置中提供的设置。
* 通过指定，创建一个或多个软件组件[INF AddComponent 指令](inf-addcomponent-directive.md)，并提供[组件 INF 文件](using-a-component-inf-file.md)。

对于这些方案在以下示例中此页上，可以找到示例代码。  另请参阅[通用驱动程序方案](../develop/universal-driver-scenarios.md)，它描述了如何[DCHU 通用驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)使用扩展 Inf。

在下图中，两家不同公司创建了单独的驱动程序包的同一设备，点线中所示。  第一个包含只需扩展 INF，并且第二个包含组件 INF 和旧软件模块。  图还显示了如何扩展 INF 可以引用的组件 INF，可以在打开引用软件模块安装。

![扩展和 INF 的组件层次结构](images/extension-component-inf-hierarchy.png)

## <a name="how-extension-inf-and-base-inf-work-together"></a>扩展 INF 和 INF 基如何协同工作

扩展 INF 中的设置将应用后基 INF 中的设置。 因此，如果扩展 INF 和基 INF 指定相同的设置，将应用扩展 INF 中的版本。 同样，如果基 INF 发生更改，则扩展 INF 将保持状态并且是应用于新的基 INF。

## <a name="specifying-extensionid"></a>指定扩展 Id

在编写扩展 INF，则生成调用的特殊 GUID **ExtensionId**，这是将项记入 INF **\[版本\]** 部分。

系统通过匹配的硬件 ID 和兼容 Id 中的一个扩展 INF 中指定的设备标识为特定设备可能扩展 Inf [**模型**](inf-models-section.md)适用于部分该系统。

在所有可能扩展指定相同的 Inf 之间**ExtensionId**值，系统将选择仅安装，并通过这些基 INF 应用其设置。  驱动程序日期和 INF 中指定的驱动程序版本，在用于排序，请选择单个 INF 之间具有相同的多个扩展 Inf **ExtensionId**。

若要说明，请考虑包括假设的设备有三个扩展 Inf 的以下方案：

![选择关系图显示如何基 INF 和 Inf 扩展](images/extension-base-inf-example.png)

**ExtensionId**值会显示在大括号和每个驱动程序[排名](how-setup-ranks-drivers--windows-vista-and-later-.md)中标题功能区中所示。

首先，系统将选择具有最新版本和最高排名的驱动程序。

接下来，系统处理可用扩展 Inf。  两个具有**ExtensionId**值`{B}`，和一个具有**ExtensionId**值`{A}`。  从最初的两个假设，驱动程序日期都相同。  下一步场加时赛是驱动程序版本，因此系统选择 v2.0 INF 扩展名。

使用唯一的扩展 INF **ExtensionId**还选择值。  系统应用的设备，基本 INF，然后应用该设备的两个扩展 Inf。

请注意扩展 INF 文件始终应用后基 INF 中，但没有应用扩展 Inf 没有确定的顺序。

## <a name="creating-an-extension-inf"></a>创建扩展 INF

以下是您需要定义作为扩展 INF INF 的条目。

1.  指定以下值作为**类**并**ClassGuid**中[**版本**](inf-version-section.md)部分。 安装程序类的详细信息，请参阅[系统定义设备安装程序类可用于供应商](https://msdn.microsoft.com/library/windows/hardware/ff553426)。

    ```cpp
    [Version]
    ...
    Class       = Extension
    ClassGuid   = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
    ```

2.  提供**ExtensionId**中的条目[ **\[版本\]** ](inf-version-section.md)部分。 生成初始版本的扩展 INF，新的 GUID 或重复使用的初始扩展 INF 的后续更新的最后一个 GUID。

    ```cpp
    ExtensionId = {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} ; replace with your own GUID
    ```

请注意，只能使用组织**ExtensionID**它拥有。  注册扩展 ID 的信息，请参阅[管理 Windows 硬件开发人员中心仪表板中的硬件提交](../dashboard/manage-your-hardware-submissions.md)。     

3.  如果要更新的扩展 INF，保留**ExtensionId**相同，增量版本或日期 （或两者） 指定为[ **DriverVer** ](inf-driverver-directive.md)指令。 为给定**ExtensionId**值，即插即用选择最高 INF **DriverVer**。

4.  在中[ **INF 模型部分**](inf-models-section.md)，指定一个或多个硬件和兼容 Id 相匹配的目标设备。  请注意，这些硬件和兼容 Id 不需要基 INF 相匹配。  通常情况下，扩展 INF 列出比基本 INF，目的是为了进一步专门化的特定驱动程序配置一个更具体的硬件 ID。  例如，基本 INF 可能使用两部分 PCI 硬件 ID，而扩展 INF 中指定由四部分组成的 PCI 硬件 ID，如下所示：
    
    ```cpp
    [DeviceExtensions.NTamd64]
    %Device.ExtensionDesc% = DeviceExtension_Install, PCI\VEN_XXXX&DEV_XXXX&SUBSYS_XXXXXXXX&REV_XXXX
    ```

    或者，扩展 INF 中可能会列出相同的硬件 ID 与基 INF，例如如果设备已非常窄目标，或者如果基 INF 已列出最具体的硬件 id。
    
    在某些情况下，扩展 INF 可能提供更具体的设备 ID，如兼容 ID，以便在更广泛的一组设备自定义的设置。

5.  未定义具有的服务`SPSVCINST_ASSOCSERVICE`。  但是，扩展 INF 可以定义其他服务，例如设备的筛选器驱动程序。  有关指定服务的详细信息，请参阅[ **INF AddService 指令**](inf-addservice-directive.md)。

在大多数情况下，您将提交扩展 INF 包到硬件开发人员中心单独从基础驱动程序包。  如何为包扩展 Inf，以及一些代码示例链接示例，请参阅[通用驱动程序方案](../develop/universal-driver-scenarios.md)。

驱动程序验证和提交过程是相同的扩展插件与正则 Inf Inf。 有关详细信息，请参阅[Windows HLK Getting Started](https://msdn.microsoft.com/library/windows/hardware/dn915002)。

## <a name="uninstalling-an-extension-driver"></a>卸载扩展驱动程序

在卸载之前扩展驱动程序，必须先卸载基础设备。  接下来，运行 PnPUtil 扩展 INF。

若要删除的驱动程序包，请使用`pnputil /delete-driver oem0.inf`。
若要强制删除驱动程序包，请使用`pnputil /delete-driver oem1.inf /force`。

## <a name="example-1-using-an-extension-inf-to-set-the-device-friendly-name"></a>示例 1：使用扩展 INF 设置设备的友好名称

在一个常见方案中，设备制造商 (IHV) 提供基本的驱动程序与基本 INF，然后系统制造商 (OEM) 提供了补充，并且在某些情况下将替代的配置和设置的基本 INF 的 INF 的扩展。  以下代码片段是完整扩展 INF 演示了如何设置设备的友好名称。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = Extension
ClassGuid   = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider    = %CONTOSO%
ExtensionId = {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} ; replace with your own GUID
DriverVer   = 05/28/2013,1.0.0.0
CatalogFile = delta.cat

[Manufacturer]
%CONTOSO% = DeviceExtensions,NTamd64

[DeviceExtensions.NTamd64]
%Device.ExtensionDesc% = DeviceExtension_Install, PCI\VEN_XXXX&DEV_XXXX&SUBSYS_XXXXXXXX&REV_XXXX

[DeviceExtension_Install]
; No changes

[DeviceExtension_Install.HW]
AddReg = FriendlyName_AddReg

[FriendlyName_AddReg]
HKR,,FriendlyName,, "New Device Friendly Name"

[Strings]
CONTOSO              = "Contoso"
Device.ExtensionDesc = "Sample Device Extension"
```

## <a name="example-2-using-an-extension-inf-to-install-additional-software"></a>示例 2：使用扩展 INF 安装其他软件

以下代码片段是包含在一个完整扩展 INF[驱动程序的通用驱动程序的包安装工具包](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)。  此示例使用[INF AddComponent 指令](inf-addcomponent-directive.md)来创建一个服务，以及可执行文件安装的组件。  可以在组件 INF 中执行的操作的详细信息，请参阅[使用组件 INF 文件](using-a-component-inf-file.md)。

若要访问此文件联机，请参阅[ `osrfx2_DCHU_extension.inx` ](https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_extension/osrfx2_DCHU_extension.inx)。

```cpp
;/*++
;
;Copyright (c) Microsoft Corporation.  All rights reserved.
;
;   THIS CODE AND INFORMATION IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY
;   KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE
;   IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A PARTICULAR
;   PURPOSE.
;
;Module Name:
;
;    osrfx2_DCHU_extension.INF
;
;Abstract:
;
;    Extension inf for the OSR FX2 Learning Kit
;
;--*/

[Version]
Signature = "$WINDOWS NT$"
Class = Extension
ClassGuid = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider = %ManufacturerName%
ExtensionId = {3846ad8c-dd27-433d-ab89-453654cd542a}
CatalogFile = osrfx2_DCHU_extension.cat
DriverVer = 05/16/2017,15.14.36.721

[Manufacturer]
%ManufacturerName% = OsrFx2Extension, NT$ARCH$

[OsrFx2Extension.NT$ARCH$]
%OsrFx2.ExtensionDesc% = OsrFx2Extension_Install, USB\Vid_045e&Pid_94aa&mi_00
%OsrFx2.ExtensionDesc% = OsrFx2Extension_Install, USB\Vid_0547&PID_1002

[OsrFx2Extension_Install.NT]
CopyInf=osrfx2_DCHU_usersvc.inf

[OsrFx2Extension_Install.NT.HW]
AddReg = OsrFx2Extension_AddReg
AddReg = OsrFx2Extension_COMAddReg

[OsrFx2Extension_AddReg]
HKR, OSR, "OperatingParams",, "-Extended"
HKR, OSR, "OperatingExceptions",, "x86"

; Add all registry keys to successfully register the
; In-Process ATL COM Server MSFT Sample.
[OsrFx2Extension_COMAddReg]
HKCR,AppID\ATLDllCOMServer.DLL,AppID,,"{9DD18FED-55F6-4741-AF25-798B90C4AED5}"
HKCR,AppID\{9DD18FED-55F6-4741-AF25-798B90C4AED5},,,"ATLDllCOMServer"
HKCR,ATLDllCOMServer.SimpleObject,,,"SimpleObject Class"
HKCR,ATLDllCOMServer.SimpleObject\CLSID,,,"{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}"
HKCR,ATLDllCOMServer.SimpleObject\CurVer,,,"ATLDllCOMServer.SimpleObject.1"
HKCR,ATLDllCOMServer.SimpleObject.1,,,"SimpleObject Class"
HKCR,ATLDllCOMServer.SimpleObject.1\CLSID,,,"{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084},,,"SimpleObject Class"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\InprocServer32,,%REG_EXPAND_SZ%,"%%SystemRoot%%\System32\ATLDllCOMServer.dll"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\InprocServer32,ThreadingModel,,"Apartment"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\ProgID,,,"ATLDllCOMServer.SimpleObject.1"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\Programmable,,%FLG_ADDREG_KEYONLY%
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\TypeLib,,,"{9B23EFED-A0C1-46B6-A903-218206447F3E}"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\VersionIndependentProgID,,,"ATLDllCOMServer.SimpleObject"

[OsrFx2Extension_Install.NT.Components]
AddComponent = osrfx2_DCHU_component,,OsrFx2Extension_ComponentInstall
AddComponent = osrfx2_DCHU_usersvc,,OsrFx2Extension_ComponentInstall_UserSvc

[OsrFx2Extension_ComponentInstall]
ComponentIds=VID_045e&PID_94ab

[OsrFx2Extension_ComponentInstall_UserSvc]
ComponentIds=VID_045e&PID_94ac

[Strings]
ManufacturerName = "Contoso"
OsrFx2.ExtensionDesc = "OsrFx2 DCHU Device Extension"
REG_EXPAND_SZ = 0x00020000
FLG_ADDREG_KEYONLY = 0x00000010
```

## <a name="example-3-using-an-extension-inf-to-install-a-filter-driver"></a>示例 3：使用扩展 INF 安装筛选器驱动程序

扩展 INF 还可用于安装设备，它使用系统提供的设备驱动程序的筛选器驱动程序。 扩展 INF 指定设备的硬件 ID，并提供服务和筛选器驱动程序设置。

下面的代码段演示如何使用扩展 INF 安装筛选器驱动程序。

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = Extension
ClassGuid   = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider    = %CONTOSO%
ExtensionId = {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} ; replace with your own GUID
DriverVer   = 05/28/2013,1.0.0.0
CatalogFile = delta.cat

[Manufacturer]
%CONTOSO% = DeviceExtensions,NTx86

[DeviceExtensions.NTx86]
%Device.ExtensionDesc% = DeviceExtension_Install,PCI\VEN_XXXX&DEV_XXXX&SUBSYS_XXXXXXXX&REV_XXXX

[DeviceExtension_Install]
CopyFiles = Filter_CopyFiles

[DeviceExtension_Install.HW]
AddReg = DeviceExtensionFilter_AddReg

[DeviceExtensionFilter_AddReg]
HKR,,"UpperFilters",0x00010008,"fltsample" 

[DeviceExtension_Install.Services]
AddService = fltsample,,FilterService_Install

[FilterService_Install]
DisplayName   = %FilterSample.ServiceDesc%
ServiceType   = 1   ; SERVICE_KERNEL_DRIVER
StartType     = 3   ; SERVICE_DEMAND_START
ErrorControl  = 1   ; SERVICE_ERROR_NORMAL
ServiceBinary = %12%\fltsample.sys

[Filter_CopyFiles]
fltsample.sys

[SourceDisksFiles]
fltsample.sys = 1

[SourceDisksNames]
1 = Disk

[DestinationDirs]
Filter_CopyFiles = 12

[Strings]
CONTOSO                  = "Contoso"
Device.ExtensionDesc     = "Sample Extension Device"
FilterSample.ServiceDesc = "Sample Upper Filter"
```

##  <a name="submitting-an-extension-inf-for-certification"></a>提交认证的扩展 INF

有关如何扩展 Inf 在硬件开发人员中心上处理的详细信息，请参阅[使用 Windows 硬件开发人员中心仪表板中的扩展 Inf](../dashboard/submit-dashboard-extension-inf-files.md)。

## <a name="related-topics"></a>相关主题

* [通用驱动程序方案](../develop/universal-driver-scenarios.md)
* [Using a Universal INF File](using-a-universal-inf-file.md)（使用通用 INF 文件）
* [开始使用通用驱动程序](../develop/getting-started-with-universal-drivers.md)
* [适用于通用驱动程序的驱动程序程序包安装工具包](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)
