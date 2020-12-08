---
title: NDIS_STATUS_PM_WOL_PATTERN_REJECTED
description: NDIS_STATUS_PM_WOL_PATTERN_REJECTED 状态向过量驱动程序的电源管理唤醒 (WOL) 模式已被拒绝。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PM_WOL_PATTERN_REJECTED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4ac539789524da9f5f9d5135e9c03eb0f99339d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837169"
---
# <a name="ndis_status_pm_wol_pattern_rejected"></a>已 \_ 拒绝 NDIS 状态 \_ PM \_ WOL \_ 模式 \_


"NDIS \_ 状态 \_ PM \_ WOL \_ 模式 \_ 已拒绝" 状态指示过量驱动程序的电源管理唤醒 (WOL) 模式已被拒绝。

<a name="remarks"></a>备注
-------

当 ndis 或微型端口驱动程序删除 WOL 模式时，它们可以生成 NDIS \_ 状态 \_ PM \_ WOL \_ 模式 \_ 拒绝的状态指示。 对于已拒绝的 WOL 模式， [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBuffer** 成员包含 ULONG 模式标识符。 NDIS 在 [**ndis \_ PM \_ WOL \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构的 **PatternId** 成员中提供了 WOL 模式标识符。

\_ \_ \_ \_ \_ 当必须从网络适配器中删除以前添加的 wol 模式时，ndis 将生成 ndis 状态 PM WOL 模式拒绝的状态指示。 例如，对于更高优先级的 WOL 模式，NDIS 可能会删除 WOL 模式以释放资源。 通知事件将仅发送到添加了删除模式的绑定。

对于使用基础结构元素跨基础结构分担模式和漫游的无线网络适配器，可能新的基础结构元素可能不支持与上一元素相同的功能。 在这种情况下，微型端口驱动程序可以向 NDIS 发出状态指示，NDIS 将发出 \_ \_ \_ \_ \_ 使用特定错误代码拒绝的 ndis 状态 PM WOL 模式。

WiFi 驱动程序可能会在本地缓存唤醒模式。 当驱动程序处理 OID 以添加或删除唤醒模式时，驱动程序可以选择仅更新其本地缓存。 驱动程序可以将基础结构的更新延迟到收到 [oid \_ PM \_ 参数](./oid-pm-parameters.md) OID。

基础结构可能没有足够的资源来容纳所有唤醒模式。 在这种情况下，基础结构可以接受唤醒模式的部分列表。 当微型端口驱动程序完成 OID \_ PM \_ 参数 set 请求时，驱动程序必须使 \_ \_ \_ \_ \_ 访问点 (AP) 拒绝的每个 WOL 模式拒绝状态指示。

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
<td><p>在 NDIS 6.20 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ PM \_ WOL \_ 模式**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID \_ PM \_ 参数](./oid-pm-parameters.md)

 

