---
title: OID_GEN_INTERRUPT_MODERATION
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_INTERRUPT_MODERATION OID 来确定是否在微型端口适配器上启用了中断裁决。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_INTERRUPT_MODERATION 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 48688e183d3cd0f390b919e2d219b4b80d2aba29
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820079"
---
# <a name="oid_gen_interrupt_moderation"></a>OID \_ 代 \_ 中断 \_ 裁决


作为查询，NDIS 和过量驱动程序使用 OID \_ GEN \_ 中断 \_ 裁决 oid 来确定是否在微型端口适配器上启用了中断裁决。 如果查询成功，NDIS 将返回 [**ndis \_ 中断 \_ 裁决 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters) 结构，其中包含当前中断裁决设置。

作为一个集，NDIS 和过量驱动程序使用 OID \_ GEN \_ 中断 \_ 裁决 OID 在微型端口适配器上启用或禁用中断裁决。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需。 集和查询。

<a name="remarks"></a>备注
-------

对于查询，如果微型端口驱动程序不支持中断裁决，则驱动程序必须在 **NdisInterruptModerationNotSupported** NDIS **InterruptModeration** \_ 中断 \_ 裁决参数结构的 InterruptModeration 成员中指定 NdisInterruptModerationNotSupported \_ 。

对于集，如果驱动程序报告 **NdisInterruptModerationNotSupported** ，以响应 OID 生成 \_ \_ 中断 \_ 裁决查询，则驱动程序应返回 NDIS \_ 状态 \_ 无效 \_ 数据以响应设置请求。 微型端口驱动程序接收 [**NDIS \_ 中断 \_ 裁决 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters) 结构。 如果将 **InterruptModeration** NDIS \_ 中断裁决参数的 InterruptModeration 成员 \_ \_ 设置为 **NdisInterruptModerationEnabled**，则微型端口驱动程序应该启用中断裁决。 否则，它应禁用中断裁决。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 中断 \_ 裁决 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)

 

