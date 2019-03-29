---
title: OID_NDK_LOCAL_ENDPOINTS
description: 为查询，NDIS 和基础驱动程序或用户模式应用程序使用 OID_NDK_LOCAL_ENDPOINTS OID 到活动的 Network Direct 侦听器和共享的终结点的列表上的微型端口适配器。
ms.assetid: 93F077AF-7FEA-4F92-9784-B65ADCC16564
ms.date: 08/08/2017
keywords: -OID_NDK_LOCAL_ENDPOINTS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 38c933f3bb7d077d9676c79a6ac45661d8514fb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564093"
---
# <a name="oidndklocalendpoints"></a>OID\_NDK\_本地\_终结点


为查询，NDIS 和基础驱动程序或用户模式应用程序使用 OID\_NDK\_本地\_终结点 OID 到活动的 Network Direct 侦听器和微型端口适配器上的共享终结点的列表。

NDIS 6.30 和更高版本的微型端口驱动程序提供 NDK 服务必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

NDIS 发出此 OID，若要从适配器获取活动的 Network Direct 侦听器和共享的终结点的列表。 适配器需要返回的侦听器和共享中的终结点列表[ **NDIS\_NDK\_本地\_终结点**](https://msdn.microsoft.com/library/windows/hardware/hh451563)结构在**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。

此结构是基于本地终结点返回的数量可变的。 中指定的本地终结点数组，作为元素计数的大小**计数**成员。

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
<td><p>支持在 NDIS 6.30 和更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_NDK\_本地\_终结点**](https://msdn.microsoft.com/library/windows/hardware/hh451563)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

 

 




