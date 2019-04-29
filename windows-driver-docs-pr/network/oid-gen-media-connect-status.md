---
title: OID_GEN_MEDIA_CONNECT_STATUS
description: 为查询，OID_GEN_MEDIA_CONNECT_STATUS OID 请求在网络上的 NIC 的连接状态。
ms.assetid: 3ed26e62-a285-4b78-91c6-7c3cc0963570
ms.date: 08/08/2017
keywords: -OID_GEN_MEDIA_CONNECT_STATUS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 72575278de3943b532989997a37fd8f3e8afcfa3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358745"
---
# <a name="oidgenmediaconnectstatus"></a>OID\_GEN\_媒体\_CONNECT\_状态


为查询，OID\_GEN\_媒体\_CONNECT\_状态 OID 请求在网络上的 NIC 的连接状态。

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

NDIS NDIS 6.0 和更高版本的微型端口驱动程序处理此 OID。

OID\_GEN\_媒体\_CONNECT\_状态 OID 请求在网络上的 NIC 的连接状态作为系统定义的以下值之一：

**NdisMediaStateConnected**

**NdisMediaStateDisconnected**

当微型端口驱动程序检测到的网络连接已丢失时，它还必须调用[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)或[ **NdisMCoIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563562)函数使用 NDIS\_状态\_媒体\_（适用于 NDIS 5.1) 断开连接或 NDIS\_状态\_链接\_具有状态**MediaConnectStateDisconnected** MediaConnectState 属性中 (ndis 6.x)。 当恢复连接时，然后必须调用**NdisM (Co) IndicateStatus**使用 NDIS\_状态\_媒体\_（适用于 NDIS 5.1) 连接或 NDIS\_状态\_链接\_具有状态**MediaConnectStateConnected** MediaConnectState 属性中 (ndis 6.x)。

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


[**NdisMCoIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563562)

[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)

 

 




