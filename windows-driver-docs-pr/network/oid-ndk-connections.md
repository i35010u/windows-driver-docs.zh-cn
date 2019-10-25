---
title: OID_NDK_CONNECTIONS
description: 作为查询，NDIS 和过量驱动程序或用户模式应用程序使用 OID_NDK_CONNECTIONS OID 从微型端口适配器查询活动网络直接连接列表。
ms.assetid: 31A0BB2B-B571-4548-A9D1-BE44687DEA37
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NDK_CONNECTIONS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9d3562c8e48966c00603093b85011dd48e366d92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844588"
---
# <a name="oid_ndk_connections"></a>OID\_NDK\_连接


作为查询，NDIS 和过量驱动程序或用户模式应用程序使用 OID\_NDK\_连接 OID 从微型端口适配器查询活动网络直接连接列表。

提供 NDK 服务的 NDIS 6.30 和更高版本的微型端口驱动程序必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

NDIS 发出此 OID 以从适配器获取活动网络直接连接的列表。 适配器必须在[**ndis\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的**InformationBuffer**成员处，返回具有[**ndis\_NDK\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_connections)结构的连接列表。

此结构是基于返回的连接数进行可变大小的。 在**count**成员中指定连接数组的大小，作为元素计数。

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
<td><p>版本</p></td>
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_NDK\_连接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_connections)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

 




