---
title: WDI_TLV_LOW_LATENCY_CONNECTION_QUALITY_PARAMETERS
description: WDI_TLV_LOW_LATENCY_CONNECTION_QUALITY_PARAMETERS 是包含低延迟连接质量参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_LOW_LATENCY_CONNECTION_QUALITY_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f3f37186e3dbeb2f0e253a29922c0b276399183a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839211"
---
# <a name="wdi_tlv_low_latency_connection_quality_parameters"></a>WDI \_ TLV \_ 低 \_ 延迟 \_ 连接 \_ 质量 \_ 参数


WDI \_ tlv \_ 低 \_ 延迟 \_ 连接 \_ 质量 \_ 参数是包含低延迟连接质量参数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0xF6

## <a name="length"></a>长度


所有包含的元素的数组的大小 (以字节为单位) 。

## <a name="values"></a>值


| 类型  | 描述                                                                                                                                                                                                                                                                            |
|-------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8 | 指定在活动扫描或其他多通道操作期间端口可以位于不同通道上的最大毫秒数。 此脱离通道的唯一实例是，如果适配器需要执行被动扫描。                                 |
| UINT8 | 指定 [ \_ \_ \_ \_ \_ 所需的 NDIS 状态 WDI 指示漫游](./ndis-status-wdi-indication-roaming-needed.md)的链接质量阈值。 当链接质量低于此阈值时，适配器可以通过需要发送 NDIS \_ 状态 \_ WDI \_ 指示 \_ 漫游 \_ 。 |

 

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

## <a name="see-also"></a>请参阅


[OID \_ WDI \_ 设置 \_ 连接 \_ 质量](./oid-wdi-set-connection-quality.md)

[需要有 NDIS \_ 状态 \_ WDI \_ 指示 \_ 漫游 \_](./ndis-status-wdi-indication-roaming-needed.md)

 

