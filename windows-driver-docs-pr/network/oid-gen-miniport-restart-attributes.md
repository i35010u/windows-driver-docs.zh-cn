---
title: OID_GEN_MINIPORT_RESTART_ATTRIBUTES
description: OID_GEN_MINIPORT_RESTART_ATTRIBUTES OID 标识了 NDIS 驱动程序堆栈中用于传播微型端口适配器重新启动属性的常规属性。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MINIPORT_RESTART_ATTRIBUTES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 8ab6f889dad69d47db8686c97ac9c6a12d0ceb2b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782245"
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

如果 [**NDIS \_ 重新启动 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)结构中的 **oid** 成员是 Oid \_ 代 \_ 微型端口 \_ 重新启动 \_ 属性，则结构的 **数据** 成员将包含 [**NDIS \_ RESTART \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_general_attributes)结构。

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

## <a name="see-also"></a>请参阅


[**NDIS \_ 重新启动 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_attributes)

[**NDIS \_ 重新启动 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_restart_general_attributes)

 

