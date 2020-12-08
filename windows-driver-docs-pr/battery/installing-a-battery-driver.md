---
title: 安装电池驱动程序
description: 安装电池驱动程序
keywords:
- 电池 miniclass 驱动程序 WDK，安装
- 电池类驱动程序 WDK，安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e351353f723542f6565764705f327d42bf2abd5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798685"
---
# <a name="installing-a-battery-driver"></a>安装电池驱动程序


## <span id="ddk_installing_a_battery_driver_dg"></span><span id="DDK_INSTALLING_A_BATTERY_DRIVER_DG"></span>


电池驱动程序的 INF 文件指定有关驱动程序及其控制的设备的信息。 所有电池设备都是电池类的成员，电池类安装程序将安装驱动程序。

本部分介绍 INF 文件中特定于电池的条目。 有关创建和分发 INF 文件和安装驱动程序的详细信息，请参阅 [创建 Inf 文件](../install/overview-of-inf-files.md) 和 [inf 文件部分和指令](../install/index.md)。

电池驱动程序的 INF 文件包括下面所述的部分。

### <a name="span-idversionspanspan-idversionspanspan-idversionspanversion"></a><span id="Version"></span><span id="version"></span><span id="VERSION"></span>版本

电池驱动程序的 INF 文件使用 [**INF 版本部分**](../install/inf-version-section.md)指定电池类及其 GUID，如以下示例中所示：

``` syntax
[Version]
Signature="$WINDOWS NT$"
Class=Battery
ClassGuid={72631e54-78a4-11d0-bcf7-00aa00b7b32a}
Provider=%MyCo%
```

请注意，必须在 [**INF 字符串部分**](../install/inf-strings-section.md) 中定义% MyCo% (未显示) 。

### <a name="span-iddestinationdirsspanspan-iddestinationdirsspanspan-iddestinationdirsspandestinationdirs"></a><span id="DestinationDirs"></span><span id="destinationdirs"></span><span id="DESTINATIONDIRS"></span>DestinationDirs

在 [**Inf DestinationDirs 部分**](../install/inf-destinationdirs-section.md)中，电池驱动程序的 Inf 指定驱动程序目录 (12) 作为所有文件的默认设置。

``` syntax
[DestinationDirs]
DefaultDestDir = 12
```

### <a name="span-idmanufacturerspanspan-idmanufacturerspanspan-idmanufacturerspanmanufacturer"></a><span id="Manufacturer"></span><span id="manufacturer"></span><span id="MANUFACTURER"></span>提供

[**INF 制造商部分**](../install/inf-manufacturer-section.md)定义设备的制造商。

``` syntax
[Manufacturer]
%MyCo%=MyCompany
```

### <a name="span-idmodelsspanspan-idmodelsspanspan-idmodelsspanmodels"></a><span id="Models"></span><span id="models"></span><span id="MODELS"></span>*机型*

" [**INF *模型* " 部分**](../install/inf-models-section.md) 指定在示例) 中显示为 *pnpid* 的电池 (PnP 硬件 ID。 如果通过 ACPI 枚举设备，此部分还必须指定显示为 *acpidevnum*) 的 EISA 样式 ID (。 有关创建这些 Id 的信息，请参阅 *高级配置和电源接口规范*，可通过 [ACPI/电源管理](https://uefi.org/acpi/specs) 网站获得。

``` syntax
[MyCompany]
%pnpid.DeviceDesc% = NewBatt_Inst,pnpid
%ACPI\acpidevnum.DeviceDesc% = NewBatt_Inst,ACPI\acpidevnum
```

### <a name="span-idddinstallspanspan-idddinstallspanspan-idddinstallspanddinstall"></a><span id="DDInstall"></span><span id="ddinstall"></span><span id="DDINSTALL"></span>*DDInstall*

在示例) 的 " [**Inf *DDInstall* " 部分**](../install/inf-ddinstall-section.md) 中 (名为 \_ "NewBatt 指令" 时， [**inf CopyFiles 指令**](../install/inf-copyfiles-directive.md) 会将电池类驱动程序 (*Battc.sys*) 并将新的 miniclass 驱动程序 (*NewBatt.sys)* 到 **DestinationDirs** 指令中指定的目标。

``` syntax
[NewBatt_Inst]
CopyFiles = @NewBatt.sys
CopyFiles = @battc.sys
```

### <a name="span-idddinstallservicesspanspan-idddinstallservicesspanspan-idddinstallservicesspanddinstallservices"></a><span id="DDInstall.Services"></span><span id="ddinstall.services"></span><span id="DDINSTALL.SERVICES"></span>*DDInstall*。服务器

[**INF *DDInstall*。服务部分**](../install/inf-ddinstall-services-section.md)包括一个 [**INF AddService 指令**](../install/inf-addservice-directive.md)，该指令指定有关电池驱动程序的其他信息。 电池驱动程序的 INF 文件应指示该驱动程序是一个内核驱动程序，该驱动程序使用正常的错误处理并在操作系统初始化期间启动。 电池驱动程序指定负载顺序组扩展基准。

``` syntax
[NewBatt_Inst.Services]
AddService = NewBatt,2,NewBatt_Service_Inst    ; function driver for the device
 
[NewBatt_Service_Inst]
DisplayName    = %NewBatt.SvcDesc%
ServiceType    = 1 ;    SERVICE_KERNEL_DRIVER
StartType      = 3 ;    SERVICE_DEMAND_START
ErrorControl   = 1 ;    SERVICE_ERROR_NORMAL%
ServiceBinary  = %12%\NewBatt.sys
```

