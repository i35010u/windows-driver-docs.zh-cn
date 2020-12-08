---
title: WDI_TLV_INDICATION_WAKE_PACKET_PATTERN_ID
description: WDI_TLV_INDICATION_WAKE_PACKET_PATTERN_ID 是一个 TLV，其中包含与唤醒数据包匹配的模式的 ID。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INDICATION_WAKE_PACKET_PATTERN_ID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e3ebe2d5cf1d52fc49c3fbf208682fadc25cfd24
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836673"
---
# <a name="wdi_tlv_indication_wake_packet_pattern_id"></a>WDI \_ TLV \_ 指示 \_ 唤醒 \_ 数据包 \_ 模式 \_ ID


WDI \_ tlv \_ 指示 \_ 唤醒 \_ 数据包 \_ 模式 \_ ID 是一个 TLV，其中包含与唤醒数据包匹配的模式的 ID。

## <a name="tlv-type"></a>TLV 类型


0xB0

## <a name="length"></a>长度


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 描述                                                                                                                                                                    |
|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 与唤醒数据包匹配的模式的 ID。 此 ID 是在添加模式时定义的， [ \_ WDI \_ 设置 " \_ 添加 \_ WOL \_ 模式](./oid-wdi-set-add-wol-pattern.md)"。 |

 

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

 

