---
title: OID_GEN_PROMISCUOUS_MODE
description: 为查询，使用 OID_GEN_PROMISCUOUS_MODE OID 确定网络接口是否为混杂 (RFC 2863 从 ifPromiscuousMode)。
ms.assetid: c3ba0908-724c-4149-a66f-5c3d41751165
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PROMISCUOUS_MODE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f8ffe058c738adab8cf03b8505f1ae5882287d59
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360807"
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

仅[NDIS 网络接口](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)提供程序，因此不微型端口驱动程序或筛选器驱动程序必须支持此 OID 作为 OID 的请求。

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
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[NDIS 网络接口 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




