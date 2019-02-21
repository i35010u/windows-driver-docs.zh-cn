---
title: OID_GEN_PROMISCUOUS_MODE
description: 为查询，使用 OID_GEN_PROMISCUOUS_MODE OID 确定网络接口是否为混杂 (RFC 2863 从 ifPromiscuousMode)。
ms.assetid: c3ba0908-724c-4149-a66f-5c3d41751165
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PROMISCUOUS_MODE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4278589603de9763b31e1d2f5365cfd8936ddeaf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544757"
---
# <a name="oidgenpromiscuousmode"></a>OID\_GEN\_PROMISCUOUS\_模式


为查询，使用 OID\_GEN\_PROMISCUOUS\_模式来确定网络接口是否是混杂的 OID (*ifPromiscuousMode*从[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)).

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 及更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 NDIS 接口提供程序仅。

<a name="remarks"></a>备注
-------

仅[NDIS 网络接口](https://msdn.microsoft.com/library/windows/hardware/ff566527)提供程序，因此不微型端口驱动程序或筛选器驱动程序必须支持此 OID 作为 OID 的请求。

如果接口提供程序返回 NDIS\_状态\_成功，如果接口接受将寻址到该接口的唯一数据包，结果值应为**FALSE**。 此值应 **，则返回 TRUE**如果接口接受所有网络数据包。

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
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[NDIS 网络接口 Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 




