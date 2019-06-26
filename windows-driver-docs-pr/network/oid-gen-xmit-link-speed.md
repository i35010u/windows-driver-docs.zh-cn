---
title: OID_GEN_XMIT_LINK_SPEED
description: 为查询，使用 OID_GEN_XMIT_LINK_SPEED OID 来确定传输链接速度的网络接口。 版本信息 Windows Vista 和 laterSupported。 NDIS 6.0 和更高版本的微型端口 driversNot 请求。 NDIS 接口提供程序仅。
ms.assetid: 0a390456-8974-4668-b624-55259c2f9e20
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_XMIT_LINK_SPEED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 06727f9838fa91d01c46ca40f66048c7536e937b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385736"
---
# <a name="oidgenxmitlinkspeed"></a>OID\_GEN\_XMIT\_LINK\_SPEED


为查询，使用 OID\_GEN\_XMIT\_链接\_速度 OID 来确定传输链接速度的网络接口。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 及更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 NDIS 接口提供程序仅。

<a name="remarks"></a>备注
-------

仅[NDIS 网络接口](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)提供程序，因此不微型端口驱动程序或筛选器驱动程序必须支持此 OID 作为 OID 的请求。

如果接口提供程序返回 NDIS\_状态\_成功后，查询的结果为 ULONG64 值，该值指示传输中每秒位数的接口的链接速度。

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

 

 




