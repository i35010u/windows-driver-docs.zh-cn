---
title: OID_GEN_LAST_CHANGE
description: 为查询，使用 OID_GEN_LAST_CHANGE OID 来确定网络接口 (RFC 2863 从 ifLastChange) 的最后一个操作的状态更改的时间。
ms.assetid: bd96d1ec-2fd0-491f-acb4-c1594ce6a084
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_LAST_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 40330e5150a2ef45be4c3057ec319fd971adbd66
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375697"
---
# <a name="oidgenlastchange"></a>OID\_GEN\_最后一个\_更改


为查询，使用 OID\_GEN\_上次\_更改 OID 来确定网络接口的最后一个操作的状态更改的时间 (*ifLastChange*从[RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)).

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 及更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 NDIS 接口提供程序仅。

<a name="remarks"></a>备注
-------

仅[NDIS 网络接口](https://msdn.microsoft.com/library/windows/hardware/ff566527)提供程序，因此不微型端口驱动程序或筛选器驱动程序必须支持此 OID 作为 OID 的请求。

此 OID 返回时，该接口进入其当前操作状态时，从上次计算机重新启动，开始。 有关操作状态的详细信息，请参阅[ **NDIS\_状态\_工序\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567406)并[OID\_常规\_OPERATIONAL\_状态](oid-gen-operational-status.md)。 若要获取当前时间，接口提供程序可以调用[ **NdisGetSystemUpTimeEx** ](https://msdn.microsoft.com/library/windows/hardware/ff562675)函数。

如果在接口的最后一个重新初始化之前输入的当前操作状态，此值应为零。 . 如果接口提供程序不会跟踪操作状态更改时，值应为零。

如果接口提供程序返回 NDIS\_状态\_成功后，查询的结果是 ULONG64 值，该值指定状态更改时间，以毫秒为单位，自上次计算机重新启动。

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


[OID\_GEN\_OPERATIONAL\_状态](oid-gen-operational-status.md)

[**NDIS\_状态\_工序\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567406)

[**NdisGetSystemUpTimeEx**](https://msdn.microsoft.com/library/windows/hardware/ff562675)

[NDIS 网络接口 Oid](https://msdn.microsoft.com/library/windows/hardware/ff566545)

 

 




