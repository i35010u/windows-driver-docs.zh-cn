---
title: OID_GEN_LINK_SPEED_EX
description: 作为查询，OID_GEN_LINK_SPEED_EX OID 提供接口的传输和接收链接速度。 Windows Vista 和 laterSupported 的版本信息。 已请求 NDIS 6.0 和更高的微型端口 driversNot。 仅适用于 NDIS 接口提供程序。
ms.assetid: 86cc281b-3898-484c-9418-4408a45ebe71
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_LINK_SPEED_EX 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a6a6bdbc7dc41b17ff7fd3390e2b934bd9fa6aec
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207209"
---
# <a name="oid_gen_link_speed_ex"></a>OID \_ GEN \_ LINK \_ 速度（ \_ 例如


作为查询，OID 生成 \_ \_ 链接 \_ 速度 EX 使用 \_ oid 提供接口的传输和接收链接速度。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

NDIS 使用此 OID 查询 [NDIS 网络接口](./ndis-network-interfaces2.md) 提供程序的链接速度。 只有 NDIS 接口提供程序（而不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 OID 请求。

此 OID 返回 [**NDIS \_ 链接 \_ 速度**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_speed) 结构中的链接速度。

微型端口驱动程序在初始化期间提供链接速度，并提供更新的链接速度和状态指示。

若要在微型端口驱动程序中指定链接速度，请设置与该小型端口驱动程序传递给[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数的[**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的**XmitLinkSpeed**和**RcvLinkSpeed**成员。

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

[NDIS 网络接口 Oid](./ndis-network-interface-oids.md)

 

