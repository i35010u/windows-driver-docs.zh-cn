---
title: OID_GEN_MEDIA_CONNECT_STATUS_EX
description: 作为查询，OID_GEN_MEDIA_CONNECT_STATUS_EX OID 返回接口的连接状态。 Windows Vista 和 laterSupported。 已请求 NDIS 6.0 和更高的微型端口 driversNot。 仅适用于 NDIS 接口提供程序。
ms.assetid: 8239616c-788a-4073-8bbe-41f493a461de
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MEDIA_CONNECT_STATUS_EX 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 29022ff224cf18cf0c8964710b678c87aae42d3f
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "82104607"
---
# <a name="oid_gen_media_connect_status_ex"></a>OID\_生成\_媒体\_连接\_状态\_，例如


作为查询\_，oid 生成\_媒体\_连接\_状态\_，例如 oid 返回接口的连接状态。

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

NDIS 使用此 OID 查询[NDIS 网络接口](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)提供程序的连接状态。 只有 NDIS 接口提供程序（而不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 OID 请求。

如果查询成功，接口提供程序将返回 NDIS\_状态\_成功，并且查询的结果可以是[**NET\_IF\_\_MEDIA CONNECT\_STATE**](https://docs.microsoft.com/windows/win32/api/ifdef/ne-ifdef-net_if_media_connect_state)枚举中的值之一。

微型端口驱动程序在初始化期间提供媒体连接状态，并提供具有状态指示的更新。

若要在微型端口驱动程序中指定连接状态，请设置该小型端口驱动程序传递给[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数的[**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的**MediaConnectState**成员。

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


[**NDIS\_微型\_端口\_适配器\_常规属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[**NET\_（\_如果\_媒体\_连接状态）**](https://docs.microsoft.com/windows/win32/api/ifdef/ne-ifdef-net_if_media_connect_state)

[NDIS 网络接口 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




