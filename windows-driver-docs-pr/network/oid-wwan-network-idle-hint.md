---
title: OID_WWAN_NETWORK_IDLE_HINT
description: OID_WWAN_NETWORK_IDLE_HINT 将提示发送到网络接口，相关数据是否应在接口上处于活动状态或空闲状态。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_NETWORK_IDLE_HINT 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ea4a2ea7b4eb898af5061508a441b4efa89c0d73
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809963"
---
# <a name="oid_wwan_network_idle_hint"></a>OID \_ WWAN \_ 网络 \_ 空闲 \_ 提示


OID \_ WWAN \_ 网络 \_ 空闲 \_ 提示向网络接口发送提示，指出数据是否应在接口上处于活动状态或空闲状态。 网络服务使用试探法来确定何时向接口发送此请求，通常在其估计时间段内会减少网络流量，或者系统输入空闲状态 (例如连接备用) 。 网络接口可以将此作为试探法的输入，以实现 "fast 休眠期间" 之类的过程。

不支持查询请求。

微型端口驱动程序必须异步处理设置请求，最初 \_ 返回 \_ \_ 原始请求所需的 NDIS 状态指示，稍后用 [**NDIS \_ WWAN \_ 网络 \_ 空闲 \_ 提示**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_idle_hint) 结构指示网络空闲提示来完成请求。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>适用于 windows 10 及更高版本的 Windows。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ WWAN \_ 网络 \_ 空闲 \_ 提示**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_network_idle_hint)

 

