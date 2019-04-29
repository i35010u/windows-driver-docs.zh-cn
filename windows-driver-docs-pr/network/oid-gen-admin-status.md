---
title: OID_GEN_ADMIN_STATUS
description: 为查询，使用 OID_GEN_ADMIN_STATUS OID 来确定接口 (RFC 2863 从 ifAdminStatus) 的管理状态。
ms.assetid: e8f45521-7419-4c11-b84b-36d4d3306fc2
ms.date: 08/08/2017
keywords: -OID_GEN_ADMIN_STATUS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5323c785ee3688a7803c69c2d6c40dace8babdfe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380699"
---
# <a name="oidgenadminstatus"></a>OID\_GEN\_管理员\_状态


为查询，使用 OID\_GEN\_管理员\_状态 OID 来确定接口的管理状态 (*ifAdminStatus*从[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054))。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 及更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 NDIS 接口提供程序仅。

<a name="remarks"></a>备注
-------

管理状态是系统管理员请求的状态。

仅[NDIS 网络接口](https://msdn.microsoft.com/library/windows/hardware/ff566527)提供程序，因此不微型端口驱动程序或筛选器驱动程序必须支持此 OID 作为 OID 的请求。

如果查询成功，接口提供程序返回 NDIS\_状态\_成功和查询的结果可以是中的值之一[ **NET\_如果\_管理员\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff568740)枚举。

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


[**NET\_IF\_ADMIN\_STATUS**](https://msdn.microsoft.com/library/windows/hardware/ff568740)

[NDIS 网络接口 Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 




