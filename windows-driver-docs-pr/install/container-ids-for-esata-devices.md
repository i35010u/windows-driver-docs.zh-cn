---
title: eSATA 设备的容器 ID
description: eSATA 设备的容器 ID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 206e27dd007727f8de7bb95f71f20f0f7fd89a07
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782957"
---
# <a name="container-ids-for-esata-devices"></a>eSATA 设备的容器 ID


外部串行高级技术附件 (eSATA) 总线无法报告容器 ID。 当 Windows 操作系统确定 eSATA 设备的设备容器分组时，它依赖 ATA 总线驱动程序返回的可移动功能。

ATA 总线驱动程序通过读取以下高级主机控制器接口 (AHCI) register bits，来确定 eSATA 设备是否可移动。

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
<td align="left"><p>HBA 功能 (CAP) # A2</p></td>
<td align="left"><p>0x000</p></td>
<td align="left"><p>5-支持外部 SATA (SXS) </p></td>
<td align="left"><p>当设置为1时，此位值指示主机总线适配器 (HBA) 有一个或多个具有一个外部可用的信号连接器的 SATA 端口 (如 eSATA 连接器) 。</p>
<p>如果此位设置为1，则软件可以引用 PxCMD 位来确定特定端口是否将其信号连接器作为仅限信号的连接器提供 (也就是说，power 不是该连接器) 的一部分。</p></td>
</tr>
<tr class="even">
<td align="left"><p>端口 x 命令和状态 (PxCMD) </p></td>
<td align="left"><p>0x18</p></td>
<td align="left"><p>18-Hot-Plug 支持的端口 (HPCP) </p></td>
<td align="left"><p>设置为1时，此位值表示端口的信号和电源连接器可通过联合信号和电源连接器从外部使用。</p>
<p></p>
<div class="alert">
<strong>注意</strong>  这仅适用于支持热插拔功能的 blindmate 连接器。
</div>
<div>
 
</div>
.</td>
</tr>
<tr class="odd">
<td align="left"><p>端口 x 命令和状态 (PxCMD) </p></td>
<td align="left"><p>0x18</p></td>
<td align="left"><p>21-外部 SATA 端口 (ESP) </p></td>
<td align="left"><p>设置为1时，此位值表示端口的信号连接器在外部可用， (例如 eSATA 连接器) 。 因此，此端口可能会遇到热插拔事件。</p>
<p>如果 ESP 设置为1，则必须将 PxCMD HPCP 位清除为0和 CAP。SXS 位必须设置为1。</p></td>
</tr>
</tbody>
</table>

 

如果满足以下任一条件，ATA 总线驱动程序会将连接到 eSATA 端口的任何设备标记为可移动：

-   HPCP 位设置为1，表示 eSATA 端口是支持热插拔操作的外部端口。

-   SXS 和 ESP 位均设置为1，这表示 SATA 端口是仅限外部信号的端口。

**注意**   这些条件是互斥的。 ESATA 端口可能会将其自身声明为外部热插拔端口或外部信号端口，但不能同时声明两者。

 

有关 SATA 和 eSATA 接口的详细信息，请参阅 [串行 ATA 高级主机控制器接口 (AHCI) 1.3 规范](https://go.microsoft.com/fwlink/p/?linkid=148284)。

 

 





