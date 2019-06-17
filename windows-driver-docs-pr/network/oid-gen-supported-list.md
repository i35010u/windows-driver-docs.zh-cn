---
title: OID_GEN_SUPPORTED_LIST
description: 为查询，OID_GEN_SUPPORTED_LIST OID 指定数组 Oid 的微型端口驱动程序或 NIC 支持的对象。
ms.assetid: 4e663204-eee0-4732-83c9-ec1dacd41034
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_SUPPORTED_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 263789fe3249bfd98b83a51fe1627351ed2d26ae
ms.sourcegitcommit: 91b989fc3256267fab89c36b1fa54ff039dcc687
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148527"
---
# <a name="oidgensupportedlist"></a>OID\_GEN\_支持\_列表


为查询，OID\_GEN\_支持\_列表 OID 指定的 Oid 的微型端口驱动程序或 NIC 支持的对象的数组。 对象包括常规、 媒体特定和特定于实现的对象。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。 请参阅[OID\_代\_支持\_列表 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff560258)。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。 请参阅[OID\_代\_支持\_列表 (NDIS 5.1)](https://msdn.microsoft.com/library/windows/hardware/ff560258)。

<a name="remarks"></a>备注
-------

NDIS 6.0 和更高版本的微型端口驱动程序不会收到此 OID 请求。 NDIS 处理此 OID 微型端口驱动程序在初始化过程中提供的缓存值。

若要在初始化期间指定的受支持的 Oid 列表，微型端口驱动程序设置**SupportedOidList**的成员[ **NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构，并将传递到结构[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数。

NDIS 将转发到使此查询的协议驱动程序提供的列表的子集。 即 NDIS 筛选任何受支持的统计信息 Oid 的列表，因为协议驱动程序永远不会使统计信息的查询。

如果微型端口驱动程序列出在其受支持的 Oid 列表中的 OID，它必须完全支持 OID。 也就是说，微型端口驱动程序必须响应查询时返回有效的数据或设置包含列表中的 Oid 的请求。 例如， [OID\_代\_统计信息](oid-gen-statistics.md)OID 是 NDIS 6.0 和更高版本的微型端口驱动程序所需的 OID。 如果微型端口驱动程序不支持统计信息中的硬件或软件，并返回不正确的统计信息，该驱动程序不能指定 OID\_常规\_其受支持的 Oid 列表中的统计信息。

中受支持的 Oid 列表可能会显示重复项。 驱动程序不需要保证在列表中每个 OID 的只有一个条目。

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


[OID\_GEN\_STATISTICS](oid-gen-statistics.md)

 

 




