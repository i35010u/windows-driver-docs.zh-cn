---
title: 常规统计信息 OID
description: 常规统计信息 OID
ms.assetid: ebdd5723-d913-4c1a-8b1f-f70e4b0080ad
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb52ac22eee4f01cbc61a145d0624274efff6126
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104626"
---
# <a name="general-statistic-oids"></a>常规统计信息 OID





下表列出了远程 NDIS 以太网设备的常规统计信息 Oid。

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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-xmit-ok" data-raw-source="[OID_GEN_XMIT_OK](./oid-gen-xmit-ok.md)">OID_GEN_XMIT_OK</a></p></td>
<td align="left"><p>传输的帧没有错误</p></td>
</tr>
<tr class="even">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-rcv-ok" data-raw-source="[OID_GEN_RCV_OK](./oid-gen-rcv-ok.md)">OID_GEN_RCV_OK</a></p></td>
<td align="left"><p>接收的帧没有错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-xmit-error" data-raw-source="[OID_GEN_XMIT_ERROR](./oid-gen-xmit-error.md)">OID_GEN_XMIT_ERROR</a></p></td>
<td align="left"><p>传输的帧出现错误</p></td>
</tr>
<tr class="even">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-rcv-error" data-raw-source="[OID_GEN_RCV_ERROR](./oid-gen-rcv-error.md)">OID_GEN_RCV_ERROR</a></p></td>
<td align="left"><p>接收的帧出现错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>必需</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-rcv-no-buffer" data-raw-source="[OID_GEN_RCV_NO_BUFFER](./oid-gen-rcv-no-buffer.md)">OID_GEN_RCV_NO_BUFFER</a></p></td>
<td align="left"><p>缺少帧，无缓冲区</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-directed-bytes-xmit" data-raw-source="[OID_GEN_DIRECTED_BYTES_XMIT](./oid-gen-directed-bytes-xmit.md)">OID_GEN_DIRECTED_BYTES_XMIT</a></p></td>
<td align="left"><p>传输的定向字节未出现错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-directed-frames-xmit" data-raw-source="[OID_GEN_DIRECTED_FRAMES_XMIT](./oid-gen-directed-frames-xmit.md)">OID_GEN_DIRECTED_FRAMES_XMIT</a></p></td>
<td align="left"><p>传输的定向帧没有错误</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-multicast-bytes-xmit" data-raw-source="[OID_GEN_MULTICAST_BYTES_XMIT](./oid-gen-multicast-bytes-xmit.md)">OID_GEN_MULTICAST_BYTES_XMIT</a></p></td>
<td align="left"><p>传输的多播字节没有错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-multicast-frames-xmit" data-raw-source="[OID_GEN_MULTICAST_FRAMES_XMIT](./oid-gen-multicast-frames-xmit.md)">OID_GEN_MULTICAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>传输的多播帧没有错误</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-broadcast-bytes-xmit" data-raw-source="[OID_GEN_BROADCAST_BYTES_XMIT](./oid-gen-broadcast-bytes-xmit.md)">OID_GEN_BROADCAST_BYTES_XMIT</a></p></td>
<td align="left"><p>传输的广播字节未出现错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-broadcast-frames-xmit" data-raw-source="[OID_GEN_BROADCAST_FRAMES_XMIT](./oid-gen-broadcast-frames-xmit.md)">OID_GEN_BROADCAST_FRAMES_XMIT</a></p></td>
<td align="left"><p>传输的广播帧没有错误</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-directed-bytes-rcv" data-raw-source="[OID_GEN_DIRECTED_BYTES_RCV](./oid-gen-directed-bytes-rcv.md)">OID_GEN_DIRECTED_BYTES_RCV</a></p></td>
<td align="left"><p>接收的定向字节没有错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-directed-frames-rcv" data-raw-source="[OID_GEN_DIRECTED_FRAMES_RCV](./oid-gen-directed-frames-rcv.md)">OID_GEN_DIRECTED_FRAMES_RCV</a></p></td>
<td align="left"><p>接收的定向帧没有错误</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-multicast-bytes-rcv" data-raw-source="[OID_GEN_MULTICAST_BYTES_RCV](./oid-gen-multicast-bytes-rcv.md)">OID_GEN_MULTICAST_BYTES_RCV</a></p></td>
<td align="left"><p>已接收多播字节，无错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-multicast-frames-rcv" data-raw-source="[OID_GEN_MULTICAST_FRAMES_RCV](./oid-gen-multicast-frames-rcv.md)">OID_GEN_MULTICAST_FRAMES_RCV</a></p></td>
<td align="left"><p>接收的多播帧未出现错误</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-broadcast-bytes-rcv" data-raw-source="[OID_GEN_BROADCAST_BYTES_RCV](./oid-gen-broadcast-bytes-rcv.md)">OID_GEN_BROADCAST_BYTES_RCV</a></p></td>
<td align="left"><p>接收的广播字节未出现错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-broadcast-frames-rcv" data-raw-source="[OID_GEN_BROADCAST_FRAMES_RCV](./oid-gen-broadcast-frames-rcv.md)">OID_GEN_BROADCAST_FRAMES_RCV</a></p></td>
<td align="left"><p>接收的广播帧未出现错误</p></td>
</tr>
<tr class="even">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-rcv-crc-error" data-raw-source="[OID_GEN_RCV_CRC_ERROR](./oid-gen-rcv-crc-error.md)">OID_GEN_RCV_CRC_ERROR</a></p></td>
<td align="left"><p>通过循环冗余检查收到的帧 (CRC) 或帧检查序列 (FCS) 错误</p></td>
</tr>
<tr class="odd">
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/network/oid-gen-transmit-queue-length" data-raw-source="[OID_GEN_TRANSMIT_QUEUE_LENGTH](./oid-gen-transmit-queue-length.md)">OID_GEN_TRANSMIT_QUEUE_LENGTH</a></p></td>
<td align="left"><p>传输队列的长度</p></td>
</tr>
</tbody>
</table>

 

