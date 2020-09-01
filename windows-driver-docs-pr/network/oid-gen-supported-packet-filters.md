---
title: OID_GEN_SUPPORTED_PACKET_FILTERS
description: NDIS 和过量驱动程序获取小型端口适配器在初始化期间可筛选的网络数据包类型。
ms.assetid: c19cecf3-ae47-4fd1-b5dc-1f3de469e548
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_SUPPORTED_PACKET_FILTERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a818f04bf44ab9eb67c80a9016caf1e09ea7e620
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217991"
---
# <a name="oid_gen_supported_packet_filters"></a>OID \_ 代 \_ 支持的 \_ 数据包 \_ 筛选器


NDIS 和过量驱动程序获取小型端口适配器在初始化期间可筛选的网络数据包类型。

**注意**   此 OID 未在 Windows Vista 和更高版本的 Windows 操作系统中实现。 有关详细信息，请参阅“备注”部分。

 

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未实现。 （请参见“备注”部分。）

<a name="remarks"></a>备注
-------

微型端口驱动程序在初始化期间提供支持的数据包筛选器。

若要指定支持的数据包筛选器，微型端口驱动程序将设置[**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的**SupportedPacketFilters**成员，并将该结构传递给[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数。

NDIS 将信息传递到[**ndis \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的**SupportedPacketFilters**成员中的协议驱动程序。

**SupportedPacketFilters**中的值是筛选器类型标志的按位 "或"。 有关筛选器类型标志的列表，请参阅 [OID \_ GEN \_ 当前 \_ 数据包 \_ 筛选器](oid-gen-current-packet-filter.md) oid。

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


[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[OID \_ GEN \_ 当前 \_ 数据包 \_ 筛选器](oid-gen-current-packet-filter.md)

 

