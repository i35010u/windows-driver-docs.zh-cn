---
title: OID_GEN_SUPPORTED_PACKET_FILTERS
description: NDIS 和过量驱动程序获取小型端口适配器在初始化期间可筛选的网络数据包类型。
ms.assetid: c19cecf3-ae47-4fd1-b5dc-1f3de469e548
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_SUPPORTED_PACKET_FILTERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6b105a29f91604fe1f64f3960c1e7fb957216753
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844596"
---
# <a name="oid_gen_supported_packet_filters"></a>OID\_代\_支持\_数据包\_筛选器


NDIS 和过量驱动程序获取小型端口适配器在初始化期间可筛选的网络数据包类型。

**请注意**  此 OID 未在 windows Vista 和更高版本的 windows 操作系统中实现。 有关详细信息，请参阅“备注”部分。

 

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未实现。 （请参见 "备注" 部分。）

<a name="remarks"></a>备注
-------

微型端口驱动程序在初始化期间提供支持的数据包筛选器。

若要指定支持的数据包筛选器，小型端口驱动程序会将[**NDIS\_微型端口\_\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的**SupportedPacketFilters**成员设置为常规\_属性结构，并将该结构传递给[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数。

在[**ndis\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的**SupportedPacketFilters**成员中，ndis 会将信息传递给协议驱动程序。

**SupportedPacketFilters**中的值是筛选器类型标志的按位 "或"。 有关筛选器类型标志的列表，请参阅[OID\_GEN\_当前\_数据包\_筛选器](oid-gen-current-packet-filter.md)OID。

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


[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[ **\_绑定\_参数的 NDIS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[OID\_代\_当前\_数据包\_筛选器](oid-gen-current-packet-filter.md)

 

 




