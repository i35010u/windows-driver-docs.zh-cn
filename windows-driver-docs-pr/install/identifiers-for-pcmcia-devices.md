---
title: PCMCIA 设备的标识符
description: PCMCIA 设备的标识符
ms.assetid: 7eaf6372-a9cc-4714-8955-52653ec57141
keywords:
- 设备标识字符串 WDK、 PCMCIA 设备
- PCMCIA 设备-设备标识字符串 WDK
- 标识符 WDK 设备、 PCMCIA 设备
- PCMCIA 设备标识符 WDK 设备安装
- 设备 Id WDK 设备安装
- 硬件 Id WDK 设备安装
- 兼容 Id WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d244ddd3d19256849ec6a7860156b87eb1c50962
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363010"
---
# <a name="identifiers-for-pcmcia-devices"></a>PCMCIA 设备的标识符





适用于个人计算机内存卡国际协会 (PCMCIA) 设备的设备 ID 可以采用多种不同形式。 对于不是多功能设备，设备标识符的格式，如下所示：

PCMCIA\\Manufacturer-Product-Crc(4)

其中：

-   *制造商*是制造商名称。

-   *产品*是该产品的名称。

PCMCIA 枚举器直接从卡片上的元组中检索这些字符串。 这两*制造商*并*产品*是不能超过 64 个字符的可变长度字符串。 *Crc(4)* 是 4 位十六进制 CRC （循环冗余检查） 校验和的卡。 不到四位数具有前导零填充。 例如，网络适配器的设备 ID 可能是这样：

PCMCIA\\MEGAHERTZ-CC10BT/2-BF05

多功能卡，每个函数都在窗体的标识符：

PCMCIA\\Manufacturer-Product-DEVd(4)-Crc(4)

子函数号 (*d(4)* 在此示例中) 是不带前导零的十进制数字。

如果卡没有制造商的名称，该标识符具有上述三种格式之一：

PCMCIA\\UNKNOWN_MANUFACTURER-Crc(4)

PCMCIA\\UNKNOWN_MANUFACTURER-DEVd(4)-Crc(4)

PCMCIA\\MTD-MemoryType(4)

以下三种替代方法的最后一个适用于而无需在卡上的制造商标识符的闪存卡。 *MemoryType(4)* 是两个 4 位十六进制数字之一：SRAM 卡 0000 和 0002 ROM 卡。

除了将各种形式的设备 ID 刚刚描述的 INF 文件[**建模部分**](inf-models-section.md)还可以包含通过将替换为 4 位十六进制循环冗余检查 (CRC) 组成的硬件 ID包含 4 位十六进制制造商代码、 连字符，以及 4 位十六进制制造商信息代码 （无论是从载入元组） 的字符串。 例如：

PCMCIA\\MEGAHERTZ-CC10BT/2-0128-0103

PCMCIA 兼容 Id 对应于通用设备 Id 中所述[通用标识符](generic-identifiers.md)部分。 目前，PCMCIA 兼容 Id 生成只有三个设备类型在下表中所述。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">PCMCIA 兼容 ID</th>
<th align="left">设备类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>PNP0600</p></td>
<td align="left"><p>在附件 (ATA) 磁盘驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p></em>PNP0D00</p></td>
<td align="left"><p>多功能 3.0 PC 卡</p></td>
</tr>
<tr class="odd">
<td align="left"><p>*PNPC200</p></td>
<td align="left"><p>调制解调器卡</p></td>
</tr>
</tbody>
</table>

 

 

 





