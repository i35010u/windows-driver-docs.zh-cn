---
title: OID_GEN_MEDIA_CONNECT_STATUS
description: 作为查询，OID_GEN_MEDIA_CONNECT_STATUS OID 请求网络上 NIC 的连接状态。
ms.assetid: 3ed26e62-a285-4b78-91c6-7c3cc0963570
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MEDIA_CONNECT_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 417fed779300e0c485d2487f9ca220d130d06e9c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834158"
---
# <a name="oid_gen_media_connect_status"></a>OID\_代\_介质\_连接\_状态


作为查询，OID\_代\_媒体\_连接\_状态 OID 请求网络上 NIC 的连接状态。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需.

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
必需.

<a name="remarks"></a>备注
-------

NDIS 处理 NDIS 6.0 和更高版本的小型小型驱动程序的此 OID。

OID\_GEN\_媒体\_连接\_状态 OID 请求网络上 NIC 的连接状态，这是以下系统定义的值之一：

**NdisMediaStateConnected**

**NdisMediaStateDisconnected**

当微型端口驱动程序检测到网络连接已丢失时，它还必须使用 NDIS\_状态调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)或[**NDISMCOINDICATESTATUSEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)函数\_MEDIA\_DISCONNECT （对于 NDIS 5.1）或 ndis**在 MediaConnectState 属性中\_** 状态\_链接\_状态（对于 NDIS 1.x）。 在恢复连接时，它必须先调用**NdisM （Co） IndicateStatus** ，并将 NDIS\_状态\_MEDIA\_CONNECT （对于 NDIS 5.1）或 NDIS\_状态\_链接\_状态与**MediaConnectStateConnected**在 MediaConnectState 属性中（对于 NDIS 1.x）。

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


[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

 

 




