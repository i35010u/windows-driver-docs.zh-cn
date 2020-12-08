---
title: OID_GEN_LAST_CHANGE
description: 作为查询，请使用 OID_GEN_LAST_CHANGE OID 确定 (ifLastChange 从 RFC 2863) 到网络接口的上次操作状态更改的时间。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_LAST_CHANGE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cc43c1b57426e02033ae5c5d57c2bbde62bbcfae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787179"
---
# <a name="oid_gen_last_change"></a>OID \_ 生成 \_ 上次 \_ 更改


作为查询，使用 OID \_ GEN \_ 最后一个 \_ 更改 OID 来确定从 [RFC 2863](https://go.microsoft.com/fwlink/p/?linkid=84054))  (*ifLastChange* 的网络接口上次操作状态更改的时间。

**版本信息**

<a href="" id="windows-vista-and-later"></a>Windows Vista 和更高版本  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 仅适用于 NDIS 接口提供程序。

<a name="remarks"></a>备注
-------

只有 [NDIS 网络接口](./ndis-network-interfaces2.md) 提供程序（因此不是微型端口驱动程序或筛选器驱动程序）才能支持此 OID 作为 oid 请求。

当接口进入当前操作状态时，此 OID 返回从上次重新启动计算机开始的时间。 有关操作状态的详细信息，请参阅 [**NDIS \_ 状态 \_ 操作系统 \_ 状态**](./ndis-status-oper-status.md) 和 [OID \_ 生成 \_ 操作 \_ 状态](oid-gen-operational-status.md)。 为获取当前时间，接口提供程序可以调用 [**NdisGetSystemUpTimeEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetsystemuptimeex) 函数。

如果在最后一次重新初始化接口之前已输入当前操作状态，此值应为零。 . 如果接口提供程序未跟踪操作状态更改时间，则该值应为零。

如果接口提供程序返回 NDIS \_ 状态 \_ SUCCESS，则查询的结果是一个 ULONG64 值，该值指定自上次计算机重新启动以来的状态更改时间（以毫秒为单位）。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ 生成 \_ 操作 \_ 状态](oid-gen-operational-status.md)

[**NDIS \_ 状态 \_ 操作系统 \_ 状态**](./ndis-status-oper-status.md)

[**NdisGetSystemUpTimeEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetsystemuptimeex)

[NDIS 网络接口 Oid](./ndis-network-interface-oids.md)

 

