---
title: OID_NDK_LOCAL_ENDPOINTS
description: 作为查询，NDIS 和过量驱动程序或用户模式应用程序使用 OID_NDK_LOCAL_ENDPOINTS OID 连接到在微型端口适配器上的活动网络直接侦听器和共享终结点列表。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NDK_LOCAL_ENDPOINTS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2a2c52f0413147a7d617179e5522c8706fc2f748
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248588"
---
# <a name="oid_ndk_local_endpoints"></a>OID \_ NDK \_ 本地 \_ 终结点


作为查询，NDIS 和过量驱动程序或用户模式应用程序使用 OID 的 " \_ NDK \_ 本地 \_ 终结点" oid 来控制活动网络直接侦听器的列表以及微型端口适配器上的共享终结点。

提供 NDK 服务的 NDIS 6.30 和更高版本的微型端口驱动程序必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

NDIS 发出此 OID 以从适配器获取活动网络直接侦听器和共享终结点的列表。 适配器需要在 ndis [**\_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)结构的 **InformationBuffer** 成员的 [**ndis \_ NDK \_ 本地 \_ 终结点**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_local_endpoints)结构中返回侦听器和共享终结点的列表。

根据返回的本地终结点的数量，此结构的大小是可变的。 本地终结点数组的大小（作为元素计数）是在 **count** 成员中指定的。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>无受支持的版本</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2012</p></td>
</tr>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ NDK \_ 本地 \_ 终结点**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_local_endpoints)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/oidrequest/ns-oidrequest-ndis_oid_request)

 

