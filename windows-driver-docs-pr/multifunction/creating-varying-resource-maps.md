---
title: 创建可变资源映射
description: 创建可变资源映射
keywords:
- 不同资源映射 WDK 多功能设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc4a7f058634a65bf1253317acd0c6f44decb65a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818409"
---
# <a name="creating-varying-resource-maps"></a>创建可变资源映射





尽管标准资源映射只能将整个父资源分配给多功能设备的子节点，但不同的资源映射允许您在 mf.sys 枚举的子级之间细分父资源。 Windows XP 和更高版本的基于 NT 的操作系统支持不同的资源映射。

例如，请考虑 PCI 总线上的多端口串行卡。 假设每个卡的 16550 UART 函数需要一组八个 i/o 端口和一个共享中断。 还假定该卡实现为单个 PCI 函数。 在这种情况下，通常需要请求单个 i/o 端口块，然后将此块拆分为八个段（每个 16550 UART 函数一个）。

除了卡的 16550 UART 函数所需的 i/o 端口和中断资源以外，还假定设备还需要内存范围和设备专用资源。

根据这些假设，mf.sys 将返回此设备的资源要求列表，如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Resourcenumber</th>
<th>资源</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>00</p></td>
<td><p><em>内存范围</em> 基本寄存器地址 (BAR) 0</p></td>
</tr>
<tr class="even">
<td><p>01</p></td>
<td><p><em>专用数据</em></p></td>
</tr>
<tr class="odd">
<td><p>02</p></td>
<td><p><em>内存范围</em> 条形1</p></td>
</tr>
<tr class="even">
<td><p>03</p></td>
<td><p><em>专用数据</em></p></td>
</tr>
<tr class="odd">
<td><p>04</p></td>
<td><p><em>I/o 端口范围</em> 条形2</p></td>
</tr>
<tr class="even">
<td><p>05</p></td>
<td><p><em>专用数据</em></p></td>
</tr>
<tr class="odd">
<td><p>06</p></td>
<td><p><em>中断</em></p></td>
</tr>
</tbody>
</table>

 

供应商使用 INF 文件指令来指定卡的 16550 UART 函数之间共享这些资源。 对于需要设备资源段的每个函数，必须使用 INF 中的 **VaryingResourceMap** 条目来创建注册表项。 下面是此设备的 INF 文件的摘录：

```cpp
[DDInstall.RegHW] 
; for each "child" function list hardware ID and resource map 
; and/or varying resource map
HKR,Child0002,HardwareID,, child0002-hardware ID
HKR,Child0002,VaryingResourceMap,1,04, 10,00,00,00, 08,00,00,00
HKR,Child0002,ResourceMap,1,06
```

包含 **VaryingResourceMap** 的行解释如下：

-   **VaryingResourceMap** 参数后的 "1" 指定注册表项的数据类型为 REG \_ BINARY。

-   "1" 后面的数字是不同的资源映射值。 "04" 表示父资源，即我们要将其分配到此子级的段。 在这种情况下，我们将向子 (分配资源 04 (BAR 2) ，这是表示每个串行端口) 八个 i/o 端口范围的资源块。

-   接下来的两个 Dword 指示资源的偏移量，以及应分配给此子级的范围的长度（秒）。 在这种情况下，将向此子端口分配8个 i/o 端口，从偏移0x10 开始到父资源。

-   如果此子级需要另一个父资源，则资源的数字、长度和偏移量将包含在第一个资源之后的 INF 的同一行中。

**Windows.applicationmodel.resources.core.resourcemap** 参数在 [创建标准资源映射](creating-standard-resource-maps.md)中进行了介绍，并指示此子资源应该获取资源06的共享，在这种情况下，它是 PCI 设备的中断。

下面是此设备的更完整示例，指定了四个子函数：

```cpp
[Version]
Signature="$Windows NT$"
Class=MultiFunction
ClassGUID={4d36e971-e325-11ce-bfc1-08002be10318}
Provider=%MYCOMPANY%
LayoutFile=layout.inf
DriverVer=1/20/2000
[ControlFlags]
ExcludeFromSelect=*
[Manufacturer]
%MYCOMPANY%=MYCOMPANY

[MYCOMPANY]
%MYCOMPANY_4PORT%=MYCOMPANY4PORT_inst, PCI\VEN_10B5&DEV_9050&SUBSYS_003112E0

[MYCOMPANY4PORT_inst]
Include = mf.inf
Needs = MFINSTALL.mf

[MYCOMPANY4PORT_inst.HW]
AddReg=MYCOMPANY4PORT_inst.RegHW

[MYCOMPANY4PORT_inst.Services]
Include = mf.inf
Needs = MFINSTALL.mf.Services

[MYCOMPANY4PORT_inst.RegHW] 
HKR,Child0000,HardwareID,,*PNP0501
HKR,Child0000,VaryingResourceMap,1,04, 00,00,00,00, 08,00,00,00
HKR,Child0000,ResourceMap,1,06
HKR,Child0001,HardwareID,,*PNP0501
HKR,Child0001,VaryingResourceMap,1,04, 08,00,00,00, 08,00,00,00
HKR,Child0001,ResourceMap,1,06
HKR,Child0002,HardwareID,,*PNP0501
HKR,Child0002,VaryingResourceMap,1,04, 10,00,00,00, 08,00,00,00
HKR,Child0002,ResourceMap,1,06
HKR,Child0003,HardwareID,,*PNP0501
HKR,Child0003,VaryingResourceMap,1,04, 18,00,00,00, 08,00,00,00
HKR,Child0003,ResourceMap,1,06

[Strings]
MYCOMPANY= "MYCOMPANY Inc."
MYCOMPANY_4PORT="MYCOMPANY 4PORT"
```

 

 




