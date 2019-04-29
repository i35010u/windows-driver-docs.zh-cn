---
title: OID_GEN_UNKNOWN_PROTOS
description: 为查询，使用 OID_GEN_UNKNOWN_PROTOS OID 来确定网络接口 (RFC 2863 从 ifInUnknownProtos) 未知协议数据包计数。
ms.assetid: a0bebd8d-c202-41f5-84be-a3056a2eeef9
ms.date: 08/08/2017
keywords: -OID_GEN_UNKNOWN_PROTOS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a2734cf101fdd279e0b8d327c56a43fd40889320
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387894"
---
# <a name="oidgenunknownprotos"></a>OID\_GEN\_未知\_PROTOS


为查询，使用 OID\_GEN\_未知\_PROTOS OID，若要确定网络接口未知协议数据包计数 (*ifInUnknownProtos*从[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)).

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 及更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 NDIS 接口提供程序仅。

<a name="remarks"></a>备注
-------

仅[NDIS 网络接口](https://msdn.microsoft.com/library/windows/hardware/ff566527)提供程序，因此不微型端口驱动程序或筛选器驱动程序必须支持此 OID 作为 OID 的请求。

未知协议的统计信息计数器指定通过接口接收的由于关联的协议是未知或不受支持而被丢弃的数据包数。

如果接口提供程序返回 NDIS\_状态\_成功后，查询的结果是一个 ULONG64 值，指定的数据包数。

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


[NDIS 网络接口 Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 




