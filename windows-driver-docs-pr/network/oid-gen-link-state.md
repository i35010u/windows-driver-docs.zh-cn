---
title: OID_GEN_LINK_STATE
description: 作为查询，NDIS 和过量驱动程序使用 OID_GEN_LINK_STATE OID 来确定微型端口适配器的当前链接状态。
ms.assetid: 75a30054-8700-4b79-902c-c8382a25c0a2
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_LINK_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 20d1c7b8b2b11fc5e4d51ee3b7fddb6be105e3a2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844618"
---
# <a name="oid_gen_link_state"></a>OID\_代\_LINK\_状态


作为查询，NDIS 和过量驱动程序使用 OID\_代\_LINK\_状态 OID 来确定微型端口适配器的当前链接状态。 微型端口驱动程序在[**NDIS\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构中接收链接状态。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 （请参见 "备注" 部分）

<a name="remarks"></a>备注
-------

微型端口驱动程序在初始化期间提供链接状态，并提供具有状态指示的更新。

若要指定链接状态，请将NDIS\_微型端口的 MediaConnectState、MediaDuplexState、 **XmitLinkSpeed**、 **RcvLinkSpeed**、 **PauseFunctions**和**AutoNegotiationFlags**成员设置[ **\_适配器\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)微型端口驱动程序传递给[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)函数的常规\_属性结构。

如果微型端口驱动程序不支持此 OID，驱动程序将返回 NDIS\_状态\_不\_支持。 如果微型端口驱动程序支持此 OID，它将返回 NDIS 中的连接状态、双工状态和链接速度[ **\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构。

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


[**NDIS\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)

[**NDIS\_微型端口\_适配器\_常规\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)

[ **\_标头的 NDIS\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)

[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)

[OID\_代\_媒体\_连接\_状态\_EX](oid-gen-media-connect-status-ex.md)

[OID\_代\_介质\_双工\_状态](oid-gen-media-duplex-state.md)

 

 




