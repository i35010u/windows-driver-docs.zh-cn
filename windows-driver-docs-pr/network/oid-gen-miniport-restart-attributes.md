---
title: OID_GEN_MINIPORT_RESTART_ATTRIBUTES
description: OID_GEN_MINIPORT_RESTART_ATTRIBUTES OID 标识了 NDIS 驱动程序堆栈中用于传播微型端口适配器重新启动属性的常规属性。
ms.assetid: 239993f6-2176-4925-aadc-44e0df66f56b
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MINIPORT_RESTART_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 35ac543cec511a6aa93390fbabe3bcbbe7ec117f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843129"
---
# <a name="oid_gen_miniport_restart_attributes"></a>OID\_代\_小型端口\_重启\_特性


OID\_代\_微型端口\_RESTART\_特性 OID 标识在 NDIS 驱动程序堆栈中传播微型端口适配器重新启动属性的常规属性。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a name="remarks"></a>备注
-------

OID\_代\_微型端口\_RESTART\_特性 OID 不用于发出 OID 查询或设置请求。

如果[**NDIS\_重启\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)结构**为 oid\_** 代\_小型端口\_重新启动\_属性，则结构的**数据**成员包含[**NDIS\_重新启动\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_general_attributes)结构。

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


[**NDIS\_重启\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)

[**NDIS\_RESTART\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_general_attributes)

 

 




