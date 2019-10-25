---
title: OID_GEN_LAST_CHANGE
description: 作为查询，使用 OID_GEN_LAST_CHANGE OID 来确定网络接口的上次操作状态更改（RFC 2863 中的 ifLastChange）的时间。
ms.assetid: bd96d1ec-2fd0-491f-acb4-c1594ce6a084
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_LAST_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e5b1e7a4b5de1802ffb7c7c750f588f9e4885bc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844622"
---
# <a name="oid_gen_last_change"></a>OID\_代\_上次\_更改


作为查询，使用 OID\_GEN\_上次\_更改 OID 来确定网络接口的上次操作状态更改的时间（ [RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054)中的*ifLastChange* ）。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

只有[NDIS 网络接口](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interfaces2)提供程序（因此不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 oid 请求。

当接口进入当前操作状态时，此 OID 返回从上次重新启动计算机开始的时间。 有关操作状态的详细信息，请参阅[**NDIS\_状态\_操作系统\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-oper-status)和[OID\_GEN\_操作\_状态](oid-gen-operational-status.md)。 为获取当前时间，接口提供程序可以调用[**NdisGetSystemUpTimeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetsystemuptimeex)函数。

如果在最后一次重新初始化接口之前已输入当前操作状态，此值应为零。 。 如果接口提供程序未跟踪操作状态更改时间，则该值应为零。

如果接口提供程序返回 NDIS\_状态\_SUCCESS，则查询的结果是一个 ULONG64 值，该值指定自上次计算机重新启动以来的状态更改时间（以毫秒为单位）。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_GEN\_操作\_状态](oid-gen-operational-status.md)

[**NDIS\_状态\_操作系统\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-oper-status)

[**NdisGetSystemUpTimeEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetsystemuptimeex)

[NDIS 网络接口 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-network-interface-oids)

 

 




