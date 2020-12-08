---
title: WDI 数据传输
description: 本部分介绍 WDI 数据传输。 本部分使用了以下术语。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e39f088318ec5c5b1d3e79d0f7b85468812c202
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840597"
---
# <a name="wdi-data-transfer"></a>WDI 数据传输


本部分介绍 WDI 数据传输。 本部分使用了以下术语。

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
<td align="left"><p>目标 WLAN 设备 (目标) </p></td>
<td align="left"><p>物理 NIC。</p></td>
</tr>
<tr class="even">
<td align="left"><p>虚拟 WLAN 设备 (端口) </p></td>
<td align="left"><p>虚拟 NIC (例如) 的 P2P 角色端口。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>WDI</p></td>
<td align="left"><p>Microsoft WLAN 组件。 它是与目标无关的组件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="" id="target-interface-layer---til-"></a>目标接口层 (等到) </p></td>
<td align="left"><p>目标特定的软件层，它通过特定于总线的 Api 与目标进行交互。 它创建和管理 DMA 通道，并提供总线抽象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RX 管理器/RxMgr</p></td>
<td align="left"><p>RxMgr 执行不会卸载到目标的接收处理步骤。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RxEngine</p></td>
<td align="left"><p>RxEngine 在目标中发送和接收数据同步消息，解释 RX 描述符格式，并管理直接硬件到 software RX DMA 的缓冲区。</p></td>
</tr>
<tr class="odd">
<td align="left"><p> TX Manager/TxMgr</p></td>
<td align="left"><p>与 WDI 兼容的驱动程序组件，用于从操作系统获取 TX 帧，并在适当的时间将其传送到 TxEngine，并将已完成的 TX 帧返回到操作系统。</p></td>
</tr>
<tr class="even">
<td align="left"><p> TxEngine</p></td>
<td align="left"><p>目标特定的软件组件，用于处理从主机到目标的 TX 数据传输，并处理来自目标的 TX 完成消息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>目标抽象层 (TAL) </p></td>
<td align="left"><p>具有 WDI 兼容驱动程序的标准化 API 但具有特定于目标的内部实现的 "底层"。 TAL 是特定于目标的特定主机软件组件的容器层，如 TxEngine 和 RxEngine。</p></td>
</tr>
</tbody>
</table>

 

 

 





