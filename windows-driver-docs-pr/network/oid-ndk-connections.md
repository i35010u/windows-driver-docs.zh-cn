---
title: OID_NDK_CONNECTIONS
description: 为查询，NDIS 和基础驱动程序或用户模式应用程序使用 OID_NDK_CONNECTIONS OID 来查询微型端口适配器中的活动网络直接连接的列表。
ms.assetid: 31A0BB2B-B571-4548-A9D1-BE44687DEA37
ms.date: 08/08/2017
keywords: -OID_NDK_CONNECTIONS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9c15dd731ddd5dec5fb1d7d67b389fe4c4ffc1e3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383600"
---
# <a name="oidndkconnections"></a>OID\_NDK\_连接


为查询，NDIS 和基础驱动程序或用户模式应用程序使用 OID\_NDK\_连接 OID，若要查询从微型端口适配器的活动网络直接连接的列表。

NDIS 6.30 和更高版本的微型端口驱动程序提供 NDK 服务必须支持此 OID。 否则，此 OID 是可选的。

<a name="remarks"></a>备注
-------

NDIS 发出此 OID，若要从适配器获取活动的网络直接连接的列表。 适配器必须返回与连接的列表[ **NDIS\_NDK\_连接**](https://msdn.microsoft.com/library/windows/hardware/hh451561)结构在**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)结构。

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


[**NDIS\_NDK\_连接**](https://msdn.microsoft.com/library/windows/hardware/hh451561)

[**NDIS\_OID\_REQUEST**](https://msdn.microsoft.com/library/windows/hardware/ff566710)

 

 




