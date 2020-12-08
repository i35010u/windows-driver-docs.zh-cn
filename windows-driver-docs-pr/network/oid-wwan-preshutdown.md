---
title: OID_WWAN_PRESHUTDOWN
description: 系统会发送 OID_WWAN_PRESHUTDOWN，通知调制解调器系统正在进入关闭阶段，并且调制解调器应完成其操作，使其能够正常关闭。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PRESHUTDOWN 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a5478251edb326405911cf9f194ef62221a94625
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808581"
---
# <a name="oid_wwan_preshutdown"></a>OID \_ WWAN \_ PRESHUTDOWN


\_ \_ 将发送 OID WWAN PRESHUTDOWN，通知调制解调器系统正在进入关闭阶段，并且调制解调器应完成其操作，使其能够正常关闭。 它仅与物理 MBB 适配器对应的端口号一起发送。 支持多个 PDP 上下文的虚拟适配器不应接收此 OID。

不支持查询请求。

微型端口驱动程序必须异步处理设置请求，最初返回原始请求 **\_ \_ \_ 所需的 ndis 状态指示** ，稍后在 MBB 驱动程序完成所有必需的调制解调器操作之前发送 [**NDIS \_ 状态 \_ WWAN \_ PRESHUTDOWN \_ 状态**](./ndis-status-wwan-preshutdown-state.md) 通知。 此设置请求具有 [**NDIS \_ WWAN \_ 集 \_ PRESHUTDOWN \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preshutdown_state) 结构。

如果微型端口驱动程序不支持此操作，则它应返回 **\_ \_ 不 \_ 受支持的 NDIS 状态** 。

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
<td><p>从 Windows 10 版本1511开始可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 状态 \_ WWAN \_ PRESHUTDOWN \_ 状态**](./ndis-status-wwan-preshutdown-state.md)

[**NDIS \_ WWAN \_ 设置 \_ PRESHUTDOWN \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_preshutdown_state)

 

