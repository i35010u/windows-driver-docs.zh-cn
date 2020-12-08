---
title: WDI_TLV_INDICATION_WAKE_PACKET
description: WDI_TLV_INDICATION_WAKE_PACKET 是包含 NDIS_STATUS_WDI_INDICATION_WAKE_REASON 的唤醒数据包的 TLV。 当 "唤醒原因" WDI_WAKE_REASON_CODE 数据包时，状态必须包括封装在 WDI_TLV_INDICATION_WAKE_PACKET 中的唤醒数据包。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INDICATION_WAKE_PACKET 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b74f9fe17228e1c078d1e0a423944f08920cd242
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786027"
---
# <a name="wdi_tlv_indication_wake_packet"></a>WDI \_ TLV \_ 指示 \_ 唤醒 \_ 数据包


WDI \_ TLV \_ 指示 \_ 唤醒 \_ 数据包是一个 TLV，其中包含用于 [NDIS \_ 状态 \_ WDI \_ 指示 \_ 唤醒 \_ 原因](./ndis-status-wdi-indication-wake-reason.md)的唤醒数据包。 当唤醒原因为 WDI \_ 唤醒 \_ 原因 \_ 代码包时，状态必须包括封装在 WDI \_ TLV \_ 指示 \_ 唤醒 \_ 数据包中的唤醒数据包。

## <a name="tlv-type"></a>TLV 类型


0x9D

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 数组必须包含1个或多个元素。

## <a name="values"></a>值


| 类型      | 描述                                                                                                                       |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

