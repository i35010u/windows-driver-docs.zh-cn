---
title: OID_GEN_MAX_LINK_SPEED
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_MAX_LINK_SPEED OID 来确定微型端口适配器支持的最大传输和接收链接速度。
ms.assetid: 4009c5c6-57ec-47f5-80d6-d69df797857f
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MAX_LINK_SPEED 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a0da4bdef2b28a7be466b22cf5dfd475efb8f5cc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216602"
---
# <a name="oid_gen_max_link_speed"></a>OID \_ 代 \_ 最大 \_ 链接 \_ 速度


作为查询，NDIS 和过量驱动程序使用 OID 第 \_ \_ MAX \_ 链接 \_ 速度 oid 来确定微型端口适配器支持的最大传输和接收链接速度。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。  (参见 "备注" 部分) 

<a name="remarks"></a>备注
-------

小型端口驱动程序在初始化期间提供最大链接速度。

若要指定最大链接速度，请设置与该小型端口驱动程序传递给[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数的[**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的**MaxXmitLinkSpeed**和**MaxRcvLinkSpeed**成员。 如果微型端口驱动程序不支持此 OID，驱动程序将返回 \_ \_ 不 \_ 受支持的 NDIS 状态。 如果微型端口驱动程序支持此 OID，它将返回 [**NDIS \_ 链接 \_ 速度**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_speed) 结构中的最大链接速度。

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

## <a name="see-also"></a>另请参阅


[**NDIS \_ 链接 \_ 速度**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_speed)

[**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

 

