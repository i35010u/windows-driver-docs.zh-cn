---
title: WDI_TLV_WAKE_PACKET_BITMAP_PATTERN
description: WDI_TLV_WAKE_PACKET_BITMAP_PATTERN 是包含 LAN 唤醒模式的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_WAKE_PACKET_BITMAP_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6221f99304e442ded38c0bcc64ae8861cbbf170e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834113"
---
# <a name="wdi_tlv_wake_packet_bitmap_pattern"></a>WDI \_ TLV \_ 唤醒 \_ 数据包 \_ 位图 \_ 模式


WDI \_ tlv \_ 唤醒 \_ 数据包 \_ 位图 \_ 模式是包含 LAN 唤醒模式的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x5B

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                         | 允许多个 TLV 实例 | 可选 | 说明                                                                  |
|----------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ 唤醒 \_ 数据包 \_ 位图 \_ 模式 \_ ID**](wdi-tlv-wake-packet-bitmap-pattern-id.md) |                                |          | 指定 LAN 唤醒模式 ID。                                        |
| [**WDI \_ TLV \_ 位图 \_ 模式**](wdi-tlv-bitmap-pattern.md)                                  |                                |          | 指定 LAN 唤醒模式。                                           |
| [**WDI \_ TLV \_ 位图 \_ 模式 \_ 掩码**](wdi-tlv-bitmap-pattern-mask.md)                       |                                |          | 指定 LAN 唤醒模式掩码。 长度为 (PatternLength + 7) /8。 |

 

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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




