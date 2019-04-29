---
title: WDI_TLV_WAKE_PACKET_BITMAP_PATTERN
description: WDI_TLV_WAKE_PACKET_BITMAP_PATTERN 是包含 LAN 唤醒模式 TLV。
ms.assetid: 5BE0F668-A3B4-4ECF-B963-EC4DD1B1A8AE
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_WAKE_PACKET_BITMAP_PATTERN 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2d6f66c1bcaaf245f63a11b83da3c7d4a59d2403
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376356"
---
# <a name="wditlvwakepacketbitmappattern"></a>WDI\_TLV\_WAKE\_PACKET\_BITMAP\_PATTERN


WDI\_TLV\_唤醒\_数据包\_位图\_模式是包含 LAN 唤醒模式 TLV。

## <a name="tlv-type"></a>TLV 类型


0x5B

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                         | 允许多个 TLV 实例 | 可选 | 描述                                                                  |
|----------------------------------------------------------------------------------------------|--------------------------------|----------|------------------------------------------------------------------------------|
| [**WDI\_TLV\_WAKE\_PACKET\_BITMAP\_PATTERN\_ID**](wdi-tlv-wake-packet-bitmap-pattern-id.md) |                                |          | 指定在 LAN 模式 id。                                        |
| [**WDI\_TLV\_BITMAP\_PATTERN**](wdi-tlv-bitmap-pattern.md)                                  |                                |          | 指定的 LAN 唤醒模式。                                           |
| [**WDI\_TLV\_BITMAP\_PATTERN\_MASK**](wdi-tlv-bitmap-pattern-mask.md)                       |                                |          | 指定的 LAN 唤醒模式掩码。 长度是 （PatternLength + 7） / 8。 |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




