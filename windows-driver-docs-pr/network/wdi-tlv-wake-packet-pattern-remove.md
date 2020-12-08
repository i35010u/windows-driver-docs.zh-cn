---
title: WDI_TLV_WAKE_PACKET_PATTERN_REMOVE
description: WDI_TLV_WAKE_PACKET_PATTERN_REMOVE 是一种 TLV，其中包含要在 OID_WDI_SET_REMOVE_WOL_PATTERN 中删除的唤醒数据包模式 ID。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_WAKE_PACKET_PATTERN_REMOVE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 29eb48b61edcd6e454368487408e984e420fd353
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821917"
---
# <a name="wdi_tlv_wake_packet_pattern_remove"></a>WDI \_ TLV \_ 唤醒 \_ 包 \_ 模式 \_ 删除


WDI \_ tlv \_ 唤醒 \_ 包 \_ 模式 \_ 删除是一个 tlv，其中包含要删除的唤醒数据包模式 ID。 [ \_ \_ \_ \_ \_ ](./oid-wdi-set-remove-wol-pattern.md)

## <a name="tlv-type"></a>TLV 类型


0x6B

## <a name="length"></a>长度


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 描述                           |
|--------|---------------------------------------|
| UINT32 | 指定唤醒数据包模式 ID。 |

 

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

 

