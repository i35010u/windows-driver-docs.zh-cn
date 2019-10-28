---
title: OID_NDK_LOCAL_ENDPOINTS
description: 作为查询，NDIS 和过量驱动程序或用户模式应用程序在微型端口适配器上的活动网络直接侦听器和共享终结点的列表中使用 OID_NDK_LOCAL_ENDPOINTS OID。
ms.assetid: 93F077AF-7FEA-4F92-9784-B65ADCC16564
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_NDK_LOCAL_ENDPOINTS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ea564c3887461fa8b61ba4b2ec72c8e0c5b181e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844108"
---
# <a name="oid_ndk_local_endpoints"></a>OID\_NDK\_本地\_终结点


作为查询，NDIS 和过量驱动程序或用户模式应用程序使用 OID\_NDK\_本地\_终结点 OID 连接到在微型端口适配器上的活动网络直接侦听器和共享终结点列表。

提供 NDK 服务的 NDIS 6.30 和更高版本的微型端口驱动程序必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

NDIS 发出此 OID 以从适配器获取活动网络直接侦听器和共享终结点的列表。 适配器**需要在 ndis** [ **\_NDK\_本地\_终结点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_local_endpoints)\_结构中返回侦听器和共享终结点的列表， [ **\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构。

根据返回的本地终结点的数量，此结构的大小是可变的。 本地终结点数组的大小（作为元素计数）是在**count**成员中指定的。

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


[**NDIS\_NDK\_本地\_终结点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_local_endpoints)

[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

 

 




