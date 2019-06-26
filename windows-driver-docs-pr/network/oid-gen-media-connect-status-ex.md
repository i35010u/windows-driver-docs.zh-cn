---
title: OID_GEN_MEDIA_CONNECT_STATUS_EX
description: 为查询，OID_GEN_MEDIA_CONNECT_STATUS_EX OID 返回接口的连接状态。 Windows Vista 和 laterSupported。 NDIS 6.0 和更高版本的微型端口 driversNot 请求。 NDIS 接口提供程序仅。
ms.assetid: 8239616c-788a-4073-8bbe-41f493a461de
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MEDIA_CONNECT_STATUS_EX 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d317fda5c069f452ae466f25f42ef41ff8af4126
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369035"
---
# <a name="oidgenmediaconnectstatusex"></a>OID\_GEN\_媒体\_CONNECT\_状态\_EX


为查询，OID\_GEN\_媒体\_CONNECT\_状态\_EX OID 返回接口的连接状态。

<a href="" id="windows-vista-and-later"></a>Windows Vista 及更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 NDIS 接口提供程序仅。

<a name="remarks"></a>备注
-------

NDIS 使用此 OID 来查询的连接状态[NDIS 网络接口](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)提供程序。 仅 NDIS 接口提供程序，并因此不微型端口驱动程序或筛选器驱动程序必须支持此 OID 作为 OID 的请求。

如果查询成功，接口提供程序返回 NDIS\_状态\_成功和查询的结果可以是中的值之一[ **NET\_如果\_媒体\_CONNECT\_状态**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_media_connect_state)枚举。

微型端口驱动程序提供媒体在初始化过程中连接状态，并提供更新与状态的指示。

若要指定微型端口驱动程序中的连接状态，请设置**MediaConnectState**的成员[ **NDIS\_微型端口\_适配器\_常规\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)微型端口驱动程序将传递给结构[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数。

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


[**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)

[**NET\_IF\_媒体\_CONNECT\_状态**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_media_connect_state)

[NDIS 网络接口 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




