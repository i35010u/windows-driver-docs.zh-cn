---
title: OID_GEN_OPERATIONAL_STATUS
description: 为查询，使用 OID_GEN_OPERATIONAL_STATUS OID 来确定网络接口 (RFC 2863 从 ifOperStatus) 的当前操作状态。
ms.assetid: fa00d449-6ec0-4e72-8d9c-a453a0b1f3e9
ms.date: 08/08/2017
keywords: -OID_GEN_OPERATIONAL_STATUS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 71160e83fc93cac0e85655c3335d4cb51674132d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377578"
---
# <a name="oidgenoperationalstatus"></a>OID\_GEN\_OPERATIONAL\_状态


为查询，使用 OID\_GEN\_OPERATIONAL\_状态 OID 来确定网络接口的当前操作状态 (*ifOperStatus*从[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)).

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 及更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 NDIS 接口提供程序仅。

<a name="remarks"></a>备注
-------

NDIS 处理此 OID 的微型端口适配器和筛选器模块，并仅[NDIS 网络接口](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)提供程序接收此 OID 查询。

如果查询成功，接口提供程序返回 NDIS\_状态\_成功和查询的结果可以是中的值之一[ **NET\_如果\_工序\_状态**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_oper_status)枚举。

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


[**NET\_IF\_OPER\_STATUS**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_oper_status)

[NDIS 网络接口 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




