---
title: OID_GEN_INTERRUPT_MODERATION
description: 为查询，NDIS 和基础驱动程序使用 OID_GEN_INTERRUPT_MODERATION OID 来确定如果微型端口适配器上启用中断裁决。
ms.assetid: 4d9d2bda-f0b3-42d5-bb49-93a9b256f5ad
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_INTERRUPT_MODERATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 898630da98e34af22aca3cc6b0d2c6e68feed0f2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369092"
---
# <a name="oidgeninterruptmoderation"></a>OID\_GEN\_中断\_审查


为查询，NDIS 和基础驱动程序使用 OID\_GEN\_中断\_审查 OID，以确定是否的微型端口适配器上启用中断裁决。 如果查询成功，返回 NDIS [ **NDIS\_中断\_审查\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)结构，其中包含当前的中断裁决设置。

作为一组 NDIS 和基础驱动程序使用 OID\_GEN\_中断\_审查 OID，若要启用或禁用微型端口适配器上的中断裁决。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需。 设置和查询。

<a name="remarks"></a>备注
-------

对于查询，如果微型端口驱动程序不支持中断裁决，驱动程序必须指定**NdisInterruptModerationNotSupported**中**InterruptModeration** NDIS 成员\_中断\_审查\_参数结构。

对于一组，如果该驱动程序报告**NdisInterruptModerationNotSupported** OID 响应\_常规\_中断\_审查查询，则驱动程序应返回 NDIS\_状态\_无效\_集请求的响应中的数据。 微型端口驱动程序收到[ **NDIS\_中断\_审查\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)结构。 如果**InterruptModeration**成员的 NDIS\_中断\_审查\_参数设置为**NdisInterruptModerationEnabled**，微型端口驱动程序应启用中断裁决。 否则，它应禁用中断裁决。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_中断\_审查\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)

 

 




