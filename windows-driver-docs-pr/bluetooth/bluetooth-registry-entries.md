---
title: 蓝牙注册表项
description: 蓝牙注册表项
ms.assetid: a4d2848d-cb3c-4413-b06f-fe4695448f6a
keywords:
- 蓝牙 WDK，注册表项
- 注册表 WDK 蓝牙
- COD_Type 子项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af0815f26312ef5412362d5fd37cf35a815f6582
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328250"
---
# <a name="bluetooth-registry-entries"></a>蓝牙注册表项


本部分介绍的类的设备 (CoD) 注册表子项和适用于蓝牙驱动程序堆栈的条目。

### <a name="span-idcodtypesubkeyspanspan-idcodtypesubkeyspancod-major-and-cod-type-values"></a><span id="cod_type_subkey"></span><span id="COD_TYPE_SUBKEY"></span>"COD 主要"和"COD 类型"值

原始设备制造商 (Oem) 可以使用**COD 主要**并**COD 类型**值以指示已启用蓝牙的 Windows 设备的设备类。 蓝牙类安装程序将根据这些注册表值的设备类设置后，远程设备可以确定是否连接到一台便携式计算机、 台式计算机，phone 等。

注册表路径**COD 主要**并**COD 类型**值是：

HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\BTHPORT\\Parameters

请注意，设置这些值更改为系统，可能无论哪个附加蓝牙无线设备蓝牙类。 可以设置**COD 主要**并**COD 类型**到`DWORD`设备类定义的值中的字段值[蓝牙 SIG 分配数字](https://www.bluetooth.com/specifications/assigned-numbers/baseband)。

蓝牙配置文件驱动程序 BthPort.sys，读取**COD 主要**并**COD 类型**值，以确定如何对设备查询响应。 这些值只会影响`COD_MAJOR_XXX`和`COD_XXX_MINOR_XXX`设备类的位。 `COD_SERVICE_XXX` Bits 不受此注册表项。

如果**COD 主要**并**COD 类型**值未设置或者被设置为无效值、 蓝牙类安装程序会将这些值设置为`COD_MAJOR_COMPUTER`和`COD_COMPUTER_MINOR_DESKTOP`分别。

### <a name="span-idscanningparameterizationsettingsspanspan-idscanningparameterizationsettingsspanspan-idscanningparameterizationsettingsspanscanning-parameterization-settings"></a><span id="Scanning_Parameterization_Settings"></span><span id="scanning_parameterization_settings"></span><span id="SCANNING_PARAMETERIZATION_SETTINGS"></span>扫描参数化设置

配置文件驱动程序可以在其配置文件驱动程序的 INF 文件，以根据给定的设备方案的特定需求来定制指定扫描参数设置为其设备。

您可以重写默认系统扫描参数通过提供一个或多个以下的扫描参数下面列出到 AddReg 指令。 如何使用此指令的详细信息可在[INF AddReg 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)。

|                           |               |           |                                                                                |
|---------------------------|---------------|-----------|--------------------------------------------------------------------------------|
| 值名称                | 在任务栏的搜索框中键入          | 最小值 | 最大值                                                                      |
| HighDutyCycleScanWindow   | DWORD 0X10001 | 0x0004    | 0x4000。 等于或小于 HighDutyCycleScanInterval 参数应为 |
| HighDutyCycleScanInterval | DWORD 0X10001 | 0x0004    | 0x4000                                                                         |
| LowDutyCycleScanWindow    | DWORD 0X10001 | 0x0004    | 0x4000。 应小于 LowDutyCycleScanInterval 参数           |
| LowDutyCycleScanInterval  | DWORD 0X10001 | 0x0004    | 0x4000                                                                         |
| LinkSupervisionTimeout    | DWORD 0X10001 | 0x000A    | 0x0C80                                                                         |
| ConnectionLatency         | DWORD 0X10001 | 0x0000    | 0x01F4                                                                         |
| ConnectionIntervalMin     | DWORD 0X10001 | 0x0006    | 0x0C80. 应为小于或等于 ConnectionIntervalMax                     |
| ConnectionIntervalMax     | DWORD 0X10001 | 0x0006    | 0x0C80                                                                         |

 

**请注意**  对扫描参数的更改对性能的蓝牙驱动产生全局影响。 不允许对以编程方式扫描参数进行更改。 使用低占空比扫描太过积极的参数可以不只产生负面影响到可用的带宽用于其他蓝牙低能耗的连接，而且还可以为蓝牙 b R/edr 规范连接。

 

 

 





