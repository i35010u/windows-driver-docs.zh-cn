---
title: 常规统计信息 OID
description: 常规统计信息 OID
ms.assetid: ebdd5723-d913-4c1a-8b1f-f70e4b0080ad
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ba17db14a0fe6374ebc2291bead3c4c8e2de469
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382762"
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-ok" data-raw-source="[OID_GEN_XMIT_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-ok)">OID_GEN_XMIT_OK</a></p></td>
<td align="left"><p>没有错误传输的帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-ok" data-raw-source="[OID_GEN_RCV_OK](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-ok)">OID_GEN_RCV_OK</a></p></td>
<td align="left"><p>接收未出现错误的帧数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-error" data-raw-source="[OID_GEN_XMIT_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-xmit-error)">OID_GEN_XMIT_ERROR</a></p></td>
<td align="left"><p>传输错误的帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-error" data-raw-source="[OID_GEN_RCV_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-error)">OID_GEN_RCV_ERROR</a></p></td>
<td align="left"><p>接收错误的帧数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-no-buffer" data-raw-source="[OID_GEN_RCV_NO_BUFFER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-no-buffer)">OID_GEN_RCV_NO_BUFFER</a></p></td>
<td align="left"><p>错过了框架，没有缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit" data-raw-source="[OID_GEN_DIRECTED_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit)">OID_GEN_DIRECTED_BYTES_XMIT</a></p></td>
<td align="left"><p>定向 じ 舱未出现错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-xmit" data-raw-source="[OID_GEN_DIRECTED_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-xmit)">OID_GEN_DIRECTED_FRAMES_XMIT</a></p></td>
<td align="left"><p>定向帧传输的没有错误</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit" data-raw-source="[OID_GEN_MULTICAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit)">OID_GEN_MULTICAST_BYTES_XMIT</a></p></td>
<td align="left"><p>没有错误传输的多播字节数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-xmit" data-raw-source="[OID_GEN_MULTICAST_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-xmit)">OID_GEN_MULTICAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>多播传输的没有错误的帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit" data-raw-source="[OID_GEN_BROADCAST_BYTES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit)">OID_GEN_BROADCAST_BYTES_XMIT</a></p></td>
<td align="left"><p>广播传输未出现错误的字节数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-xmit" data-raw-source="[OID_GEN_BROADCAST_FRAMES_XMIT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-xmit)">OID_GEN_BROADCAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>广播传输的没有错误的帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv" data-raw-source="[OID_GEN_DIRECTED_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv)">OID_GEN_DIRECTED_BYTES_RCV</a></p></td>
<td align="left"><p>定向无错误接收的字节数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-rcv" data-raw-source="[OID_GEN_DIRECTED_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-directed-frames-rcv)">OID_GEN_DIRECTED_FRAMES_RCV</a></p></td>
<td align="left"><p>定向接收不包含错误的帧数</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv" data-raw-source="[OID_GEN_MULTICAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv)">OID_GEN_MULTICAST_BYTES_RCV</a></p></td>
<td align="left"><p>接收未出现错误的多播字节数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-rcv" data-raw-source="[OID_GEN_MULTICAST_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-multicast-frames-rcv)">OID_GEN_MULTICAST_FRAMES_RCV</a></p></td>
<td align="left"><p>多播接收到不包含错误的帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv" data-raw-source="[OID_GEN_BROADCAST_BYTES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv)">OID_GEN_BROADCAST_BYTES_RCV</a></p></td>
<td align="left"><p>广播未出现错误接收的字节数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-rcv" data-raw-source="[OID_GEN_BROADCAST_FRAMES_RCV](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-broadcast-frames-rcv)">OID_GEN_BROADCAST_FRAMES_RCV</a></p></td>
<td align="left"><p>广播接收不包含错误的帧数</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-crc-error" data-raw-source="[OID_GEN_RCV_CRC_ERROR](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-rcv-crc-error)">OID_GEN_RCV_CRC_ERROR</a></p></td>
<td align="left"><p>使用循环冗余检查 (CRC) 或框架接收到的帧检查顺序 (FCS) 错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-transmit-queue-length" data-raw-source="[OID_GEN_TRANSMIT_QUEUE_LENGTH](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-transmit-queue-length)">OID_GEN_TRANSMIT_QUEUE_LENGTH</a></p></td>
<td align="left"><p>传输队列的长度</p></td>
</tr>
</tbody>
</table>

 

 

 





