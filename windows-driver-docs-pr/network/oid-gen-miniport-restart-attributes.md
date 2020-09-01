---
title: OID_GEN_MINIPORT_RESTART_ATTRIBUTES
description: OID_GEN_MINIPORT_RESTART_ATTRIBUTES OID 标识了 NDIS 驱动程序堆栈中用于传播微型端口适配器重新启动属性的常规属性。
ms.assetid: 239993f6-2176-4925-aadc-44e0df66f56b
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MINIPORT_RESTART_ATTRIBUTES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: eaa342d77d98c84b0c7b12646a7cdf1c1d21ebfd
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207197"
---
# <a name="oid_gen_miniport_restart_attributes"></a>OID \_ 代 \_ 微型端口 \_ 重新启动 \_ 属性


OID \_ 代 \_ 微型端口 \_ RESTART \_ 属性 OID 标识在 NDIS 驱动程序堆栈中传播微型端口适配器重新启动属性的常规属性。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a name="remarks"></a>备注
-------

OID \_ 代 \_ 微型端口 \_ RESTART \_ 特性 OID 不用于发出 OID 查询或设置请求。

如果[**NDIS \_ 重新启动 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)结构中的**oid**成员是 Oid \_ 代 \_ 微型端口 \_ 重新启动 \_ 属性，则结构的**数据**成员将包含[**NDIS \_ RESTART \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_general_attributes)结构。

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


[**NDIS \_ 重新启动 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)

[**NDIS \_ 重新启动 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_general_attributes)

 

