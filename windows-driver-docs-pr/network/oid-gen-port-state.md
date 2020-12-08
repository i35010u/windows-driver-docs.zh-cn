---
title: OID_GEN_PORT_STATE
description: 作为查询，过量驱动程序使用 OID_GEN_PORT_STATE OID 获取在 NDIS_OID_REQUEST 结构的 PortNumber 成员中指定的端口的当前状态。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PORT_STATE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ad65a21e14c5b2a2edd420bfe449caa41ac5272e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829441"
---
# <a name="oid_gen_port_state"></a>OID \_ 生成 \_ 端口 \_ 状态


作为查询，过量驱动程序使用 OID 生成 \_ \_ 端口 \_ 状态 OID 获取在 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **PortNumber** 成员中指定的端口的当前状态。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。  (参见 "备注" 部分) 

<a name="remarks"></a>备注
-------

NDIS 处理此 OID 和微型端口驱动程序不会收到此 OID 查询。

如果查询成功，NDIS 将返回 NDIS \_ 状态 \_ 成功，并返回 [**ndis \_ 端口 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state) 结构中的端口状态信息。

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


[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 端口 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)

 

