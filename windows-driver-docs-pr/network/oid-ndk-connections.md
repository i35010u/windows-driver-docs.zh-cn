---
title: OID_NDK_CONNECTIONS
description: 为查询，NDIS 和基础驱动程序或用户模式应用程序使用 OID_NDK_CONNECTIONS OID 来查询微型端口适配器中的活动网络直接连接的列表。
ms.assetid: 31A0BB2B-B571-4548-A9D1-BE44687DEA37
ms.date: 08/08/2017
keywords: -OID_NDK_CONNECTIONS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 18e42347613cce87fbda1cd96d48e4fde11b88fd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373909"
---
# <a name="oidndkconnections"></a>OID\_NDK\_连接


为查询，NDIS 和基础驱动程序或用户模式应用程序使用 OID\_NDK\_连接 OID，若要查询从微型端口适配器的活动网络直接连接的列表。

NDIS 6.30 和更高版本的微型端口驱动程序提供 NDK 服务必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

NDIS 发出此 OID，若要从适配器获取活动的网络直接连接的列表。 适配器必须返回与连接的列表[ **NDIS\_NDK\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ndk_connections)结构在**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构。

此结构是可变的基于返回的连接数。 中指定连接数组，作为元素计数的大小**计数**成员。

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
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_NDK\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ndk_connections)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

 

 




