---
title: OID_GEN_SUPPORTED_PACKET_FILTERS
description: NDIS 和基础驱动程序获取的微型端口适配器可以筛选在初始化期间的网络数据包的类型。
ms.assetid: c19cecf3-ae47-4fd1-b5dc-1f3de469e548
ms.date: 08/08/2017
keywords: -OID_GEN_SUPPORTED_PACKET_FILTERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 87debd95e54b258fdaed5beb4b47a8395da2f227
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386992"
---
# <a name="oidgensupportedpacketfilters"></a>OID\_GEN\_支持\_数据包\_筛选器


NDIS 和基础驱动程序获取的微型端口适配器可以筛选在初始化期间的网络数据包的类型。

**请注意**  Windows Vista 和更高版本的 Windows 操作系统中未实现此 OID。 有关详细信息，请参阅“备注”部分。

 

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未实现。 （请参见备注部分。）

<a name="remarks"></a>备注
-------

微型端口驱动程序在初始化过程中提供的受支持的数据包筛选器。

若要指定受支持的数据包筛选器，微型端口驱动程序设置**SupportedPacketFilters**的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构，并将传递到结构[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数。

NDIS 将信息传递到协议驱动程序中**SupportedPacketFilters**的成员[ **NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)结构。

中的值**SupportedPacketFilters**是类型标志的位或运算的筛选器。 有关筛选器类型标志的列表，请参阅[OID\_代\_当前\_数据包\_筛选器](oid-gen-current-packet-filter.md)OID。

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


[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)

[**NDIS\_BIND\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[OID\_GEN\_CURRENT\_PACKET\_FILTER](oid-gen-current-packet-filter.md)

 

 




