---
title: OID_GEN_MEDIA_DUPLEX_STATE
description: 作为查询，OID_GEN_MEDIA_DUPLEX_STATE OID 返回接口的双工状态。 Windows Vista 和 laterSupported 的版本信息。 已请求 NDIS 6.0 和更高的微型端口 driversNot。 仅适用于 NDIS 接口提供程序。
ms.assetid: 63776227-dc48-4506-888f-c4b944837c4c
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MEDIA_DUPLEX_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 30f2bfa421e52ef3091fec615b1fec89a82468d5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834150"
---
# <a name="oid_gen_media_duplex_state"></a>OID\_代\_介质\_双工\_状态


作为查询，OID\_代\_媒体\_双工\_状态 OID 返回接口的双工状态。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

NDIS 使用此 OID 查询[NDIS 网络接口](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)提供程序的双工状态。 只有 NDIS 接口提供程序（而不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 OID 请求。

如果查询成功，接口提供程序将\_\_状态返回 NDIS 状态，并且[**如果\_媒体\_双工\_状态**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_media_duplex_state)枚举，则查询的结果可能是 NET\_中的值之一。

微型端口驱动程序在初始化期间提供媒体双工状态，并提供具有状态指示的更新。

若要在微型端口驱动程序中指定双工状态，请将[**NDIS\_微型端口\_\_\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)的**MediaDuplexState**成员设置为微型端口驱动程序传递到[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数。

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


[**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**如果\_介质\_双工\_状态，则为 NET\_** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_media_duplex_state)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[NDIS 网络接口 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




