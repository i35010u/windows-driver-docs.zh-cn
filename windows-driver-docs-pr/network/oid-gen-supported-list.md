---
title: OID_GEN_SUPPORTED_LIST
description: 作为查询，OID_GEN_SUPPORTED_LIST OID 为微型端口驱动程序或 NIC 支持的对象指定 Oid 数组。
ms.assetid: 4e663204-eee0-4732-83c9-ec1dacd41034
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_SUPPORTED_LIST 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8b5b5632c9a55720b6530163ca59c5d9806478c6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844597"
---
# <a name="oid_gen_supported_list"></a>OID\_GEN\_支持\_列表


作为查询，支持的 OID\_GEN\_支持\_列表 OID 为微型端口驱动程序或 NIC 支持的对象指定 Oid 数组。 对象包括常规、特定于媒体和特定于实现的对象。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需. 请参阅[支持 OID\_GEN\_支持\_列表（NDIS 5.1）](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff560258(v=vs.85))。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需. 请参阅[支持 OID\_GEN\_支持\_列表（NDIS 5.1）](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff560258(v=vs.85))。

<a name="remarks"></a>备注
-------

NDIS 6.0 和更高版本的微型端口驱动程序不会收到此 OID 请求。 NDIS 使用小型端口驱动程序在初始化期间提供的缓存值处理此 OID。

若要在初始化期间指定支持的 Oid 列表，微型端口驱动程序将设置[**NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的**SupportedOidList**成员，并将该结构传递到[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数。

NDIS 将提供的列表的一个子集转发到执行此查询的协议驱动程序。 也就是说，NDIS 筛选出列表中任何受支持的统计信息 Oid，因为协议驱动程序从不进行统计查询。

如果微型端口驱动程序在其支持的 Oid 列表中列出了 OID，则它必须完全支持 OID。 也就是说，微型端口驱动程序在响应查询或为列表中包含的 Oid 设置请求时必须返回有效的数据。 例如， [oid\_GEN\_STATISTICS](oid-gen-statistics.md) OID 是 NDIS 6.0 和更高的微型端口驱动程序的必需 oid。 如果微型端口驱动程序不支持硬件或软件中的统计信息，并且返回错误的统计信息，则驱动程序无法在其支持的 Oid 列表中指定 OID\_代\_统计信息。

重复项可能出现在支持的 Oid 列表中。 驱动程序不需要确保列表中的每个 OID 只有一个条目。

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


[OID\_代\_统计信息](oid-gen-statistics.md)

 

 




