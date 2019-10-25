---
title: OID_GEN_INTERRUPT_MODERATION
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_INTERRUPT_MODERATION OID 来确定是否在微型端口适配器上启用了中断裁决。
ms.assetid: 4d9d2bda-f0b3-42d5-bb49-93a9b256f5ad
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_INTERRUPT_MODERATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ee23d7219250a5bbc78caaef3fd2415d298d299d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843630"
---
# <a name="oid_gen_interrupt_moderation"></a>OID\_代\_中断\_裁决


作为查询，NDIS 和过量驱动程序使用 OID\_代\_中断\_裁决 OID 来确定是否在微型端口适配器上启用了中断裁决。 如果查询成功，NDIS 将返回[**ndis\_中断\_裁决\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)包含当前中断裁决设置的参数结构。

作为集，NDIS 和过量驱动程序使用 OID\_代\_中断\_裁决 OID，以启用或禁用微型端口适配器上的中断裁决。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
必需. 集和查询。

<a name="remarks"></a>备注
-------

对于查询，如果微型端口驱动程序不支持中断裁决，则驱动程序必须在 NDIS\_中断\_裁决的**InterruptModeration**成员中指定**NdisInterruptModerationNotSupported**\_参数结构。

对于集，如果驱动程序报告**NdisInterruptModerationNotSupported**为响应 OID\_代\_中断\_裁决查询，则驱动程序应返回 NDIS\_状态\_无效的数据，以响应设置请求。 微型端口驱动程序接收[**NDIS\_中断\_裁决\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)结构。 如果 NDIS\_中断的**InterruptModeration**成员\_裁决\_参数设置为**NdisInterruptModerationEnabled**，则微型端口驱动程序应该启用中断裁决。 否则，它应禁用中断裁决。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[ **\_裁决\_参数的 NDIS\_中断**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_interrupt_moderation_parameters)

 

 




