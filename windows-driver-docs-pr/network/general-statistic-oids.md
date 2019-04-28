---
title: 常规统计信息 OID
description: 常规统计信息 OID
ms.assetid: ebdd5723-d913-4c1a-8b1f-f70e4b0080ad
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35fd0aea63406a37355fd12967cbdc510640104e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349899"
---
# <a name="general-statistic-oids"></a>常规统计信息 OID





下表列出了适用于远程 NDIS 以太网设备的常规统计信息 Oid。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">支持</th>
<th align="left">OID</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569656" data-raw-source="[OID_GEN_XMIT_OK](https://msdn.microsoft.com/library/windows/hardware/ff569656)">OID_GEN_XMIT_OK</a></p></td>
<td align="left"><p>没有错误传输的帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569632" data-raw-source="[OID_GEN_RCV_OK](https://msdn.microsoft.com/library/windows/hardware/ff569632)">OID_GEN_RCV_OK</a></p></td>
<td align="left"><p>接收未出现错误的帧数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569654" data-raw-source="[OID_GEN_XMIT_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569654)">OID_GEN_XMIT_ERROR</a></p></td>
<td align="left"><p>传输错误的帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569629" data-raw-source="[OID_GEN_RCV_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569629)">OID_GEN_RCV_ERROR</a></p></td>
<td align="left"><p>接收错误的帧数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569631" data-raw-source="[OID_GEN_RCV_NO_BUFFER](https://msdn.microsoft.com/library/windows/hardware/ff569631)">OID_GEN_RCV_NO_BUFFER</a></p></td>
<td align="left"><p>错过了框架，没有缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569578" data-raw-source="[OID_GEN_DIRECTED_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569578)">OID_GEN_DIRECTED_BYTES_XMIT</a></p></td>
<td align="left"><p>定向 じ 舱未出现错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569580" data-raw-source="[OID_GEN_DIRECTED_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569580)">OID_GEN_DIRECTED_FRAMES_XMIT</a></p></td>
<td align="left"><p>定向帧传输的没有错误</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569612" data-raw-source="[OID_GEN_MULTICAST_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569612)">OID_GEN_MULTICAST_BYTES_XMIT</a></p></td>
<td align="left"><p>没有错误传输的多播字节数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569614" data-raw-source="[OID_GEN_MULTICAST_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569614)">OID_GEN_MULTICAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>多播传输的没有错误的帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569440" data-raw-source="[OID_GEN_BROADCAST_BYTES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569440)">OID_GEN_BROADCAST_BYTES_XMIT</a></p></td>
<td align="left"><p>广播传输未出现错误的字节数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569442" data-raw-source="[OID_GEN_BROADCAST_FRAMES_XMIT](https://msdn.microsoft.com/library/windows/hardware/ff569442)">OID_GEN_BROADCAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>广播传输的没有错误的帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569577" data-raw-source="[OID_GEN_DIRECTED_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569577)">OID_GEN_DIRECTED_BYTES_RCV</a></p></td>
<td align="left"><p>定向无错误接收的字节数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569579" data-raw-source="[OID_GEN_DIRECTED_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569579)">OID_GEN_DIRECTED_FRAMES_RCV</a></p></td>
<td align="left"><p>定向接收不包含错误的帧数</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569611" data-raw-source="[OID_GEN_MULTICAST_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569611)">OID_GEN_MULTICAST_BYTES_RCV</a></p></td>
<td align="left"><p>接收未出现错误的多播字节数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569613" data-raw-source="[OID_GEN_MULTICAST_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569613)">OID_GEN_MULTICAST_FRAMES_RCV</a></p></td>
<td align="left"><p>多播接收到不包含错误的帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569439" data-raw-source="[OID_GEN_BROADCAST_BYTES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569439)">OID_GEN_BROADCAST_BYTES_RCV</a></p></td>
<td align="left"><p>广播未出现错误接收的字节数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569441" data-raw-source="[OID_GEN_BROADCAST_FRAMES_RCV](https://msdn.microsoft.com/library/windows/hardware/ff569441)">OID_GEN_BROADCAST_FRAMES_RCV</a></p></td>
<td align="left"><p>广播接收不包含错误的帧数</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569627" data-raw-source="[OID_GEN_RCV_CRC_ERROR](https://msdn.microsoft.com/library/windows/hardware/ff569627)">OID_GEN_RCV_CRC_ERROR</a></p></td>
<td align="left"><p>使用循环冗余检查 (CRC) 或框架接收到的帧检查顺序 (FCS) 错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569646" data-raw-source="[OID_GEN_TRANSMIT_QUEUE_LENGTH](https://msdn.microsoft.com/library/windows/hardware/ff569646)">OID_GEN_TRANSMIT_QUEUE_LENGTH</a></p></td>
<td align="left"><p>传输队列的长度</p></td>
</tr>
</tbody>
</table>

 

 

 





