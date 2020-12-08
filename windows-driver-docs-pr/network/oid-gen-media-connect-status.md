---
title: OID_GEN_MEDIA_CONNECT_STATUS
description: 作为查询，OID_GEN_MEDIA_CONNECT_STATUS OID 请求网络上 NIC 的连接状态。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MEDIA_CONNECT_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bf8eab2354f8cfd72368ae183da0ed14a3489c41
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820059"
---
# <a name="oid_gen_media_connect_status"></a>OID \_ 生成 \_ 媒体 \_ 连接 \_ 状态


作为查询，OID 生成 \_ \_ 媒体 \_ 连接 \_ 状态 OID 请求网络上 NIC 的连接状态。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需。

<a name="remarks"></a>备注
-------

NDIS 处理 NDIS 6.0 和更高版本的小型小型驱动程序的此 OID。

OID 生成 \_ \_ 媒体 \_ 连接 \_ 状态 OID 将网络上 NIC 的连接状态请求为以下系统定义的值之一：

**NdisMediaStateConnected**

**NdisMediaStateDisconnected**

当微型端口驱动程序检测到网络连接已丢失时，它还必须调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 或 [**NdisMCoIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex) 函数，该函数具有 NDIS 5.1) 的 ndis \_ 状态 \_ MEDIA \_ 断开连接 (，或 \_ 在 \_ \_ ndis **MediaConnectStateDisconnected**) 的 MediaConnectState (属性中使用的 ndis 状态链接状态。 在恢复连接时，它必须为 ndis 5.1) 调用 **NdisM (Co) IndicateStatus** ，并将 ndis \_ 状态 \_ MEDIA \_ CONNECT (用于 ndis，或 \_ 将 Ndis 状态 \_ 链接 \_ 状态与 **MediaConnectStateConnected** MediaConnectState 属性 (用于 ndis 1.x) 。

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


[**NdisMCoIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)

[**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

 

