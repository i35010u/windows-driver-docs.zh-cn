---
title: WDI_TLV_INDICATION_WAKE_PACKET
description: WDI_TLV_INDICATION_WAKE_PACKET 是包含 NDIS_STATUS_WDI_INDICATION_WAKE_REASON 的唤醒数据包的 TLV。 当 "唤醒原因" WDI_WAKE_REASON_CODE 数据包时，状态必须包括封装在 WDI_TLV_INDICATION_WAKE_PACKET 中的唤醒数据包。
ms.assetid: 3C566FED-4594-403F-93D4-1CA6F2F655F9
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INDICATION_WAKE_PACKET 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 45b3bd35118b9677d54013dbed84b1bf475ae3fc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212717"
---
# <a name="wdi_tlv_indication_wake_packet"></a>WDI \_ TLV \_ 指示 \_ 唤醒 \_ 数据包


WDI \_ TLV \_ 指示 \_ 唤醒 \_ 数据包是一个 TLV，其中包含用于 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 唤醒 \_ 原因](./ndis-status-wdi-indication-wake-reason.md)的唤醒数据包。 当唤醒原因为 WDI \_ 唤醒 \_ 原因 \_ 代码包时，状态必须包括封装在 WDI \_ TLV \_ 指示 \_ 唤醒 \_ 数据包中的唤醒数据包。

## <a name="tlv-type"></a>TLV 类型


0x9D

## <a name="length"></a>Length


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 说明                                                                                                                       |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------|
| UINT8\[\] | 唤醒数据包。 大小是将在正常接收路径中指示的数据包的平面内存版本大小。 |

 

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

 

