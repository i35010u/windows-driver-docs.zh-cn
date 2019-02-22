---
title: 创建不同的资源映射
description: 创建不同的资源映射
ms.assetid: bfe3a760-d8fe-4213-9bbe-2bad6927d8e2
keywords:
- 不同的资源映射 WDK 多功能设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a02047076db951b88d87b4af4f4404c66ee2bcc6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541555"
---
# <a name="creating-varying-resource-maps"></a>创建不同的资源映射





尽管标准版资源映射只能将整个父资源分配一个子级的多功能设备，不同的资源映射使您细分之间 mf.sys 枚举的子级的父资源。 在 Windows XP 和更高版本的基于 NT 的操作系统上支持不同的资源映射。

例如，考虑 PCI 总线上的多端口串行卡。 假定每个卡的 16550 UART 函数需要一组 8 个 I/O 端口和共享的中断。 另外，假设卡作为单个 PCI 函数。 在此方案中，通常会请求一个独立的 I/O 端口块，然后将此块拆分为八个段，一个用于每个 16550 UART 函数。

除了此卡的 16550 UART 功能所需的 I/O 端口和中断资源，假定该设备还要求设备专用资源和内存范围。

根据这些假设，mf.sys 将返回此设备，按以下方式构造资源要求列表：

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
<td><p><em>内存范围</em>基寄存器地址 （栏） 0</p></td>
</tr>
<tr class="even">
<td><p>01</p></td>
<td><p><em>专用数据</em></p></td>
</tr>
<tr class="odd">
<td><p>02</p></td>
<td><p><em>内存范围</em>条形图 1</p></td>
</tr>
<tr class="even">
<td><p>03</p></td>
<td><p><em>专用数据</em></p></td>
</tr>
<tr class="odd">
<td><p>04</p></td>
<td><p><em>I/O 端口范围</em>条形图 2</p></td>
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

 

供应商使用 INF 文件指令来指定这些资源在卡的 16550 UART 函数之间共享。 对于每个函数都需要一个段的设备的资源，必须使用**VaryingResourceMap** INF 创建注册表项中的条目。 下面是此设备 INF 文件的摘录：

```cpp
[DDInstall.RegHW] 
; for each "child" function list hardware ID and resource map 
; and/or varying resource map
HKR,Child0002,HardwareID,, child0002-hardware ID
HKR,Child0002,VaryingResourceMap,1,04, 10,00,00,00, 08,00,00,00
HKR,Child0002,ResourceMap,1,06
```

行包含**VaryingResourceMap**解释，如下所示：

-   "1"的以下**VaryingResourceMap**参数指定的注册表项的数据类型是 REG\_二进制。

-   后面"1"的数字是不同的资源映射值。 "04"指示父资源中，我们将分配到此子段。 在这种情况下，我们正在将资源 04 的段 (条形图 2) 分配给子 （即，一种表示每个串行端口的八个 I/O 端口范围的资源）。

-   接下来两个 dword 值指示，首先中的资源，第二个，应分配给此子范围的长度的偏移量。 在这种情况下，8 个 I/O 端口分配到此子到父资源的偏移量 0x10 开始。

-   如果此子需要另一个父资源，资源的数量、 长度和偏移量将包含 INF 中，在同一行后的第一个资源。

**ResourceMap**参数描述[创建标准资源映射](creating-standard-resource-maps.md)，并指示此子级，应获取的共享资源 06，在这种情况下即 PCI 设备的中断。

下面是此设备，指定四个子函数的更完整示例：

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

 

 




