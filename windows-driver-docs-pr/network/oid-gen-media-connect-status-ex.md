---
title: OID_GEN_MEDIA_CONNECT_STATUS_EX
description: 作为查询，OID_GEN_MEDIA_CONNECT_STATUS_EX OID 返回接口的连接状态。 Windows Vista 和 laterSupported。 已请求 NDIS 6.0 和更高的微型端口 driversNot。 仅适用于 NDIS 接口提供程序。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MEDIA_CONNECT_STATUS_EX 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 15b5256377a16624917386d47e48cb682bbdcb9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820075"
---
# <a name="oid_gen_media_connect_status_ex"></a>OID \_ 生成 \_ 媒体 \_ 连接 \_ 状态， \_ 例如


作为查询，OID 生成 \_ \_ 媒体 \_ 连接状态， \_ \_ 例如 oid 返回接口的连接状态。

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

NDIS 使用此 OID 查询 [NDIS 网络接口](./ndis-network-interfaces2.md) 提供程序的连接状态。 只有 NDIS 接口提供程序（而不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 OID 请求。

如果查询成功，接口提供程序将返回 NDIS \_ 状态 \_ 成功，并且查询的结果可以是 [**NET \_ IF \_ MEDIA \_ CONNECT \_ STATE**](/windows/win32/api/ifdef/ne-ifdef-net_if_media_connect_state) 枚举中的值之一。

微型端口驱动程序在初始化期间提供媒体连接状态，并提供具有状态指示的更新。

若要在微型端口驱动程序中指定连接状态，请设置该小型端口驱动程序传递给 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数的 [**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)结构的 **MediaConnectState** 成员。

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


[**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[**NET （ \_ 如果 \_ 媒体 \_ 连接 \_ 状态）**](/windows/win32/api/ifdef/ne-ifdef-net_if_media_connect_state)

[NDIS 网络接口 Oid](./ndis-network-interface-oids.md)

 

