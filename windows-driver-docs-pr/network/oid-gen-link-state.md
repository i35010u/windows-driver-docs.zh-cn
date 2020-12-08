---
title: OID_GEN_LINK_STATE
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_LINK_STATE OID 来确定微型端口适配器的当前链接状态。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_LINK_STATE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 99f76f8a01856f9195a1c9d4c05669b7493688b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827563"
---
# <a name="oid_gen_link_state"></a>OID \_ 生成 \_ 链接 \_ 状态


作为查询，NDIS 和过量驱动程序使用 OID \_ GEN \_ 链接 \_ 状态 oid 来确定微型端口适配器的当前链接状态。 微型端口驱动程序接收 [**NDIS \_ 链接 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state) 结构中的链接状态。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。  (参见 "备注" 部分) 

<a name="remarks"></a>备注
-------

微型端口驱动程序在初始化期间提供链接状态，并提供具有状态指示的更新。

若要指定链接状态，请设置 **MediaConnectState**、 **MediaDuplexState**、 **XmitLinkSpeed**、 **RcvLinkSpeed**、 **PauseFunctions** 和 **AutoNegotiationFlags** 成员，其中， [**微型 \_ 端口 \_ 适配器的 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes) 结构是微型端口驱动程序传递给 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数的。

如果微型端口驱动程序不支持此 OID，驱动程序将返回 \_ \_ 不 \_ 受支持的 NDIS 状态。 如果微型端口驱动程序支持此 OID，它将返回 [**NDIS \_ 链接 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state) 结构中的连接状态、双工状态和链接速度。

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


[**NDIS \_ 链接 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)

[**NDIS \_ 微型端口 \_ 适配器 \_ 常规 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[**NDIS \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)

[**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[OID \_ 生成 \_ 媒体 \_ 连接 \_ 状态， \_ 例如](oid-gen-media-connect-status-ex.md)

[OID \_ 生成 \_ 介质 \_ 双工 \_ 状态](oid-gen-media-duplex-state.md)

 

