---
title: OID_GEN_PORT_STATE
description: 作为查询，过量驱动程序使用 OID_GEN_PORT_STATE OID 获取在 NDIS_OID_REQUEST 结构的 PortNumber 成员中指定的端口的当前状态。
ms.assetid: e0705b2e-08ea-4ed4-a6df-4c33b934c3dd
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PORT_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2e3064a8fc5e1200ab50dce57f519a0165fd1141
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824379"
---
# <a name="oid_gen_port_state"></a>OID\_GEN\_端口\_状态


作为查询，过量驱动程序使用 OID\_GEN\_端口\_状态 OID 获取在[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**PortNumber**成员中指定的端口的当前状态。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 （请参见 "备注" 部分）

<a name="remarks"></a>备注
-------

NDIS 处理此 OID 和微型端口驱动程序不会收到此 OID 查询。

如果查询成功，NDIS 会将 NDIS\_状态恢复\_成功，并返回[**ndis\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)结构中的端口状态信息。

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


[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_state)

 

 




