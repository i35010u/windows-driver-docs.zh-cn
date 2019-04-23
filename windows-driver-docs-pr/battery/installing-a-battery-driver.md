---
title: 安装电池驱动程序
description: 安装电池驱动程序
ms.assetid: 09db4d88-0cac-4171-8d05-d15a2cf4dab4
keywords:
- 电池 miniclass 驱动程序 WDK，安装
- 电池类驱动程序 WDK，安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c8f35af8987f85a66fc647377dfa48ead17e5a5
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903975"
---
# <a name="installing-a-battery-driver"></a>安装电池驱动程序


## <span id="ddk_installing_a_battery_driver_dg"></span><span id="DDK_INSTALLING_A_BATTERY_DRIVER_DG"></span>


电池驱动程序的 INF 文件指定有关该驱动程序和它控制的设备的信息。 所有电池设备电池类的成员并且电池类安装程序会安装该驱动程序。

本部分介绍特定于电池的 INF 文件中的条目。 有关创建和分发 INF 文件和安装驱动程序的详细信息，请参阅[创建一个 INF 文件](https://msdn.microsoft.com/library/windows/hardware/ff549520)并[INF 文件的部分和指令](https://msdn.microsoft.com/library/windows/hardware/ff547433)。

电池驱动程序的 INF 文件包含如下所述的部分。

### <a name="span-idversionspanspan-idversionspanspan-idversionspanversion"></a><span id="Version"></span><span id="version"></span><span id="VERSION"></span>版本

电池驱动程序的 INF 文件指定电池类和其 GUID，使用[ **INF 版本部分**](https://msdn.microsoft.com/library/windows/hardware/ff547502)，如以下示例所示：

``` syntax
[Version]
Signature="$WINDOWS NT$"
Class=Battery
ClassGuid={72631e54-78a4-11d0-bcf7-00aa00b7b32a}
Provider=%MyCo%
```

请注意 %%必须中定义的 MyCo [ **INF 字符串部分**](https://msdn.microsoft.com/library/windows/hardware/ff547485) （未显示）。

### <a name="span-iddestinationdirsspanspan-iddestinationdirsspanspan-iddestinationdirsspandestinationdirs"></a><span id="DestinationDirs"></span><span id="destinationdirs"></span><span id="DESTINATIONDIRS"></span>DestinationDirs

在中[ **INF DestinationDirs 部分**](https://msdn.microsoft.com/library/windows/hardware/ff547383)，电池驱动程序的 INF 驱动程序目录 (12) 指定的所有文件的默认值。

``` syntax
[DestinationDirs]
DefaultDestDir = 12
```

### <a name="span-idmanufacturerspanspan-idmanufacturerspanspan-idmanufacturerspanmanufacturer"></a><span id="Manufacturer"></span><span id="manufacturer"></span><span id="MANUFACTURER"></span>制造商

[ **INF 制造商部分**](https://msdn.microsoft.com/library/windows/hardware/ff547454)定义设备制造商。

``` syntax
[Manufacturer]
%MyCo%=MyCompany
```

### <a name="span-idmodelsspanspan-idmodelsspanspan-idmodelsspanmodels"></a><span id="Models"></span><span id="models"></span><span id="MODELS"></span>*模型*

[ **INF*模型*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547456)指定电池的即插即用硬件 ID (显示为*pnpid*在示例中)。 如果通过 ACPI 枚举设备时，本部分还必须指定 EISA 样式 ID (此处所示*acpidevnum*)。 有关创建这些 Id 的信息，请参阅*高级配置和电源接口规范*，可通过[ACPI / 电源管理](https://uefi.org/acpi/specs)网站。

``` syntax
[MyCompany]
%pnpid.DeviceDesc% = NewBatt_Inst,pnpid
%ACPI\acpidevnum.DeviceDesc% = NewBatt_Inst,ACPI\acpidevnum
```

### <a name="span-idddinstallspanspan-idddinstallspanspan-idddinstallspanddinstall"></a><span id="DDInstall"></span><span id="ddinstall"></span><span id="DDINSTALL"></span>*DDInstall*

在[ **INF *DDInstall*部分**](https://msdn.microsoft.com/library/windows/hardware/ff547344) (名为 NewBatt\_独占指令在示例中)，则[ **INF CopyFiles 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546346)将复制的电池类驱动程序 (*Battc.sys*) 和新 miniclass 驱动程序 (*NewBatt.sys*) 中指定的目标为**DestinationDirs**指令。

``` syntax
[NewBatt_Inst]
CopyFiles = @NewBatt.sys
CopyFiles = @battc.sys
```

### <a name="span-idddinstallservicesspanspan-idddinstallservicesspanspan-idddinstallservicesspanddinstallservices"></a><span id="DDInstall.Services"></span><span id="ddinstall.services"></span><span id="DDINSTALL.SERVICES"></span>*DDInstall*.Services

[ **INF *DDInstall*。服务部分**](https://msdn.microsoft.com/library/windows/hardware/ff547349)包括[ **INF AddService 指令**](https://msdn.microsoft.com/library/windows/hardware/ff546326) ，它指定有关电池的驱动程序的其他信息。 电池驱动程序的 INF 文件应指示驱动程序是使用正常的错误处理和启动的操作系统的初始化过程的内核驱动程序。 电池驱动程序指定加载顺序组扩展基。

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

 

 




