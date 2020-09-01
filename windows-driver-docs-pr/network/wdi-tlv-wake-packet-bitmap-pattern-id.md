---
title: WDI_TLV_WAKE_PACKET_BITMAP_PATTERN_ID
description: WDI_TLV_WAKE_PACKET_BITMAP_PATTERN_ID 是包含 LAN 唤醒模式 ID 的 TLV。
ms.assetid: 78807D91-189B-4E66-B3DC-500E9A59AEF2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_WAKE_PACKET_BITMAP_PATTERN_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: efecaa51da2c9e63c2fdc939c1bb79ab0e3329c2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215419"
---
# <a name="wdi_tlv_wake_packet_bitmap_pattern_id"></a>WDI \_ TLV \_ 唤醒 \_ 数据包 \_ 位图 \_ 模式 \_ ID


WDI \_ tlv \_ 唤醒 \_ 数据包 \_ 位图 \_ 模式 \_ ID 是包含 LAN 唤醒模式 id 的 tlv。

模式 ID 是 OS 提供的值，用于标识 LAN 唤醒模式，并且设置为在网络适配器上的 LAN 唤醒模式中唯一的值。 模式 ID 是在 OS 向底层驱动程序发送添加或完成对过量驱动程序的请求之前设置的。

## <a name="tlv-type"></a>TLV 类型


0xE3

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明                 |
|--------|-----------------------------|
| UINT32 | LAN 唤醒模式 ID。 |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ WDI \_ 设置 \_ 添加 \_ WOL \_ 模式](./oid-wdi-set-add-wol-pattern.md)

 

