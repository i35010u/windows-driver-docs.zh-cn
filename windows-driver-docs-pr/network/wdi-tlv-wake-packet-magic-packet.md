---
title: WDI_TLV_WAKE_PACKET_MAGIC_PACKET
description: WDI_TLV_WAKE_PACKET_MAGIC_PACKET 是一个 TLV，其中包含用于 OID_WDI_SET_ADD_WOL_PATTERN 的幻数据包的模式 ID。
ms.assetid: F1DEB65B-8DD4-4D4A-9DCB-950C3B562F0A
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_WAKE_PACKET_MAGIC_PACKET 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9bee6ba1f0f1db2b4705ee1ecbd30e5e076c665e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215411"
---
# <a name="wdi_tlv_wake_packet_magic_packet"></a>WDI \_ TLV \_ 唤醒 \_ 数据包 \_ 幻 \_ 数据包


WDI \_ tlv \_ 唤醒 \_ 数据包 \_ 幻 \_ 数据包是一个 TLV，其中包含用于 [OID \_ WDI \_ 集 \_ 添加 \_ WOL \_ 模式](./oid-wdi-set-add-wol-pattern.md)的幻数据包的模式 ID。

## <a name="tlv-type"></a>TLV 类型


0x5C

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明                                        |
|--------|----------------------------------------------------|
| UINT32 | 指定 LAN 唤醒幻数据包模式 ID。 |

 

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

 

