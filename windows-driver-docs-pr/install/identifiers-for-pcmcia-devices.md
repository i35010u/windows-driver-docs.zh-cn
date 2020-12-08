---
title: PCMCIA 设备的标识符
description: PCMCIA 设备的标识符
keywords:
- 设备标识字符串 WDK，PCMCIA 设备
- 标识字符串 WDK 设备，PCMCIA 设备
- 标识符 WDK 设备，PCMCIA 设备
- PCMCIA 设备标识符 WDK 设备安装
- 设备 Id WDK 设备安装
- 硬件 Id WDK 设备安装
- 兼容 Id WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a728c39674cd0bb01f1814e09a3ca5506a95d40a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829917"
---
# <a name="identifiers-for-pcmcia-devices"></a>PCMCIA 设备的标识符





对于个人计算机内存卡 (PCMCIA) 设备的国际关联，设备 ID 可以采用多种不同的形式。 对于不是多功能的设备，设备标识符的格式如下：

PCMCIA \\ 制造商-产品-Crc (4) 

其中：

-   *制造商* 是制造商的名称。

-   *Product* 是产品的名称。

PCMCIA 枚举器直接从卡上的元组中检索这些字符串。 *制造商* 和 *产品* 都是长度不超过64个字符的可变长度字符串。 *Crc (4)* 是4位十六进制 Crc (循环冗余检查来) 检查卡的校验和。 小于四位数的数字具有前导零填充。 例如，网络适配器的设备 ID 可能是：

PCMCIA \\ 兆赫-CC10BT/2-BF05

对于多功能卡，每个函数都具有以下形式的标识符：

PCMCIA \\ 制造商-产品-DEVd (4) Crc (4) 

在此示例中，子函数编号 (*d (4)*) 是不带前导零的十进制数。

如果卡没有制造商名称，则标识符具有以下三种形式之一：

PCMCIA \\ UNKNOWN_MANUFACTURER Crc (4) 

PCMCIA \\ UNKNOWN_MANUFACTURER-DEVd (4) Crc (4) 

PCMCIA \\ MTD-MemoryType (4) 

这三种替代方法中的最后一个是用于闪存卡，无需使用制造商标识符。 *MemoryType (4)* 是 2 4 位十六进制数字之一：0000表示 SRAM 卡，0002用于 ROM 卡。

除了刚才介绍的各种形式的设备 ID 之外，INF 文件的 [**型号部分**](inf-models-section.md) 还可以包含一个硬件 ID，该 id 通过将4位数的十六进制循环冗余)  (检查替换为包含4位十六进制制造商代码的字符串、连字符和4位数的十六进制制造商信息代码（从机载元组)  (）。 例如：

PCMCIA \\ 兆赫-CC10BT/2-0128-0103

PCMCIA 兼容 Id 对应于 [一般标识符](generic-identifiers.md) 部分中提到的通用设备 id。 目前，仅为三种设备类型生成 PCMCIA 兼容 Id，如下表所述。

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
<td align="left"><p>ATA) 磁盘驱动程序的 AT 附件 (</p></td>
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

 

 

 





