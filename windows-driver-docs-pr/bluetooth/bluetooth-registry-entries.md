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
ms.openlocfilehash: e5298f160a02d80ff6d04a61ce374e8130d2fb09
ms.sourcegitcommit: 20a89aa2cb2c6385c2a49ebf78e5797c821d87ab
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473723"
---
# <a name="bluetooth-registry-entries"></a>蓝牙注册表项

本部分介绍适用于蓝牙驱动程序堆栈的设备类（货到日志）注册表子项和条目。

## <a name="cod-major-and-cod-type-values"></a>"带货货的主要" 和 "货货类型" 值

原始设备制造商（Oem）可以使用 "**货到付款**" 的 "主要" 和 "**货货" 类型**值来指示已启用 Bluetooth 的 Windows 设备的设备类。 Bluetooth 类安装程序根据这些注册表值设置设备类后，远程设备可以确定它是连接到便携式计算机、台式计算机、电话等。

指向**货到货**到货到货货货的**类型**值的注册表路径为：

HKEY \_ 本地 \_ 计算机 \\ 系统 \\ CurrentControlSet \\ Services \\ BTHPORT \\ 参数

请注意，设置这些值将更改系统的设备的蓝牙类，而不考虑可能附加的蓝牙收音机。 你可以将**货到货**到货**到货到**货到货到货 `DWORD` 到的[Bluetooth SIG Assigned Numbers](https://www.bluetooth.com/specifications/assigned-numbers/baseband/)

蓝牙配置文件驱动程序 BthPort.sys，读取 "**货至货到货货货货货货货货货货货货货****货"** 这些值仅影响 `COD_MAJOR_XXX` `COD_XXX_MINOR_XXX` 设备类的和位。 `COD_SERVICE_XXX`此注册表项不影响位。

如果 "**货到货货货货货货货货货货货货货货货****的值"** 或设置为无效值，则蓝牙类安装程序会将这些值分别设置为 `COD_MAJOR_COMPUTER` 和 `COD_COMPUTER_MINOR_DESKTOP` 。

## <a name="scanning-parameterization-settings"></a>扫描参数化设置

配置文件驱动程序可以在其配置文件驱动程序的 INF 文件中指定其设备的扫描参数设置，以根据给定设备方案的特定需求进行定制。

可以通过将下面列出的一个或多个以下扫描参数提供给 AddReg 指令来覆盖默认系统扫描参数。 有关如何使用此指令的详细信息，请参阅[INF AddReg 指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)。

| 值名称                | 类型          | 最小值 | 最大值                                                                      |
|----|----|----|----|
| HighDutyCycleScanWindow   | DWORD 0x10001 | 0x0004    | 0x4000. 应等于或小于 HighDutyCycleScanInterval 参数 |
| HighDutyCycleScanInterval | DWORD 0x10001 | 0x0004    | 0x4000                                                                         |
| LowDutyCycleScanWindow    | DWORD 0x10001 | 0x0004    | 0x4000. 应小于 LowDutyCycleScanInterval 参数           |
| LowDutyCycleScanInterval  | DWORD 0x10001 | 0x0004    | 0x4000                                                                         |
| LinkSupervisionTimeout    | DWORD 0x10001 | 0x000A    | 0x0C80                                                                         |
| ConnectionLatency         | DWORD 0x10001 | 0x0000    | 0x01F4                                                                         |
| ConnectionIntervalMin     | DWORD 0x10001 | 0x0006    | 0x0C80. 应小于或等于 ConnectionIntervalMax                     |
| ConnectionIntervalMax     | DWORD 0x10001 | 0x0006    | 0x0C80                                                                         |

>[!NOTE]
>更改扫描参数会对蓝牙堆栈的性能产生全局影响。 不允许以编程方式对扫描参数进行更改。 使用太低的低责任循环扫描参数不仅会对其他蓝牙低能耗连接的可用带宽产生负面影响，还会对蓝牙 BR/EDR 连接产生负面影响。
