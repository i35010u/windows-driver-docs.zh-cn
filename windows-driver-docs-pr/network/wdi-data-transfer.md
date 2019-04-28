---
title: WDI 数据传输
description: 本部分介绍 WDI 数据传输。 在本部分中使用了以下术语。
ms.assetid: DA07E2C2-6478-40DD-AAD8-8ABD2777CA73
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf0f24cd1218d67c1ea763f4dcbf29e86e572192
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330521"
---
# <a name="wdi-data-transfer"></a>WDI 数据传输


本部分介绍 WDI 数据传输。 在本部分中使用了以下术语。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>目标 WLAN 设备 （目标）</p></td>
<td align="left"><p>物理 nic。</p></td>
</tr>
<tr class="even">
<td align="left"><p>虚拟 WLAN 设备 （端口）</p></td>
<td align="left"><p>虚拟 NIC （例如，P2P 角色端口）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WDI</p></td>
<td align="left"><p>Microsoft WLAN 组件。 它是不可知的目标组件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="" id="target-interface-layer---til-"></a>目标接口层 (TIL)</p></td>
<td align="left"><p>通过特定于总线的 Api 的目标与一个特定于目标的软件层。 它创建和管理 DMA 通道并提供总线抽象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RX 管理器 / RxMgr</p></td>
<td align="left"><p>RxMgr 执行接收到的目标将不会卸载的处理步骤。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RxEngine</p></td>
<td align="left"><p>RxEngine 发送和接收来自目标的数据同步消息，解释 RX 描述符格式，并管理直接硬件到软件 RX DMA 的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p> TX 管理器 / TxMgr</p></td>
<td align="left"><p>WDI 兼容的驱动程序组件，可从操作系统获取 TX 帧在适当的时间，将其交付给 TxEngine 并返回到操作系统的已完成的 TX 帧。</p></td>
</tr>
<tr class="even">
<td align="left"><p> TxEngine</p></td>
<td align="left"><p>处理从主机到目标，TX 数据传输和处理从目标 TX 完成消息特定于目标的软件组件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>目标抽象层 （谈论）</p></td>
<td align="left"><p>"较低的边缘"的具有标准化的 API 到 WDI 兼容的驱动程序，但具有特定于目标的内部实现。 谈论是单独的特定于目标的主机软件组件，如 TxEngine 和 RxEngine 容器层。</p></td>
</tr>
</tbody>
</table>

 

 

 





