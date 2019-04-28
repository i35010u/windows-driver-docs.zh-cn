---
title: eSATA 设备的容器 ID
description: eSATA 设备的容器 ID
ms.assetid: 991836f1-936c-4051-ac3b-ad491a4ca221
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaed1ce1561160010eb92b57bc375a277155c142
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346801"
---
# <a name="container-ids-for-esata-devices"></a>eSATA 设备的容器 ID


外部串行高级技术附件 (eSATA) 总线无法报告是容器 id。 当 Windows 操作系统确定 eSATA 设备分组的设备容器时，它依赖于 ATA 总线驱动程序返回的可移动功能。

ATA 总线驱动程序确定 eSATA 设备是通过阅读以下高级主机控制器接口 (AHCI) 注册位可移动。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">AHCI 注册</th>
<th align="left">字节偏移量</th>
<th align="left">位位置</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>HBA 功能 (CAP)）</p></td>
<td align="left"><p>0x000</p></td>
<td align="left"><p>5-支持外部 SATA (SXS)</p></td>
<td align="left"><p>设置为 1 时，此位值表示主机总线适配器 (HBA) 具有一个或多个 SATA 端口 （如 eSATA 连接器） 可从外部的仅限信号的连接器。</p>
<p>如果此位设置为 1，软件可以引用要确定特定的端口是否具有仅限信号的连接器以从外部使用其信号连接器的 PxCMD.ESP 位 （即，power 不属于该连接器）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>命令和状态 (PxCMD) 的端口</p></td>
<td align="left"><p>0x18</p></td>
<td align="left"><p>18-热插拔支持端口 (HPCP)</p></td>
<td align="left"><p>设置为 1 时，此位值指示该端口的信号和电源连接器是通过联合信号和电源连接器从外部使用。</p>
<p></p>
<div class="alert">
<strong>请注意</strong>  这仅适用于支持热即插即用功能的 blindmate 连接器。
</div>
<div>
 
</div>
.</td>
</tr>
<tr class="odd">
<td align="left"><p>命令和状态 (PxCMD) 的端口</p></td>
<td align="left"><p>0x18</p></td>
<td align="left"><p>21-外部 SATA 端口 (ESP)</p></td>
<td align="left"><p>设置为 1 时，此位值指示该端口的信号连接器是从外部使用仅限信号的连接器 （如 eSATA 连接器） 上。 因此，该端口可能会遇到热即插即用事件。</p>
<p>如果 ESP 设置为 1，则必须为 0，上限清除 PxCMD.HPCP 位。SXS 位必须设置为 1。</p></td>
</tr>
</tbody>
</table>

 

ATA 总线驱动程序将标记连接到为可移动 eSATA 端口中，如果以下项之一为 true 的任何设备：

-   HPCP 位设置为 1，指示 eSATA 端口是支持热插拔操作的外部端口。

-   SXS 和 ESP 位都将设置为 1，指示 SATA 端口是外部的仅限信号的端口。

**请注意**  这些条件是互相排斥。 ESATA 端口可能会将其自身是声明外部的热插拔-支持的端口或外部的仅限信号的端口，但不是能同时。

 

有关 SATA 和 eSATA 接口的详细信息，请参阅[串行 ATA 高级主机控制器接口 (AHCI) 1.3 规范](https://go.microsoft.com/fwlink/p/?linkid=148284)。

 

 





