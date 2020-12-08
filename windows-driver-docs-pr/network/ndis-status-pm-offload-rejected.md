---
title: NDIS_STATUS_PM_OFFLOAD_REJECTED
description: NDIS_STATUS_PM_OFFLOAD_REJECTED 状态向过量驱动程序指示电源管理协议卸载被拒绝。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PM_OFFLOAD_REJECTED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bed915c3d0374604c67afcaae0e89c2b27f28a4c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837179"
---
# <a name="ndis_status_pm_offload_rejected"></a>已 \_ 拒绝 NDIS 状态 \_ PM \_ 卸载 \_


NDIS \_ 状态 \_ PM \_ 卸载 \_ 已拒绝状态指示过量驱动程序已拒绝电源管理协议卸载。

<a name="remarks"></a>备注
-------

当 ndis 或微型端口驱动程序 \_ \_ 删除已卸载的协议时，它们可以生成 ndis 状态 PM \_ 卸载 \_ 已拒绝状态指示。 对于已拒绝的协议卸载， [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBuffer** 成员包含 ULONG。 NDIS 在 [**ndis \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的 **ProtocolOffloadId** 成员中提供了协议卸载标识符。

\_ \_ \_ \_ 当必须从网络适配器中删除以前卸载的协议时，ndis 会生成 ndis 状态 PM 卸载已拒绝的状态指示。 例如，对于更高优先级的协议卸载，NDIS 可能会删除协议卸载以释放资源。 NDIS 将状态指示发送到卸载被拒绝的协议卸载的绑定，但不会将其发送到其他绑定。

微型端口驱动程序报告此状态指示以拒绝先前接受的协议卸载。 例如，对于 WiFi WOL 事例， \_ \_ \_ \_ 如果由于供应商特定基础结构支持) 而不 (需要 PTK/GTK 旋转，则微型端口驱动程序必须使 NDIS 状态 PM 卸载已拒绝状态指示。

对于使用基础结构元素跨基础结构卸载协议和漫游的无线网络适配器，可能新的基础结构元素可能不支持与上一元素相同的功能。 在这种情况下，微型端口驱动程序可以向 NDIS 发出状态指示，NDIS 将发出 \_ \_ \_ \_ 拒绝特定错误代码的 ndis 状态 PM 卸载。

WiFi 驱动程序可以在本地缓存协议卸载请求。 当驱动程序处理 OID 以添加或删除协议卸载时，驱动程序可以选择仅更新其本地缓存。 驱动程序可以将基础结构的更新延迟到收到 [oid \_ PM \_ 参数](./oid-pm-parameters.md) OID。

基础结构可能没有足够的资源来容纳所有协议卸载。 在这种情况下，基础结构可以接受部分协议卸载。 当微型端口驱动程序完成 OID \_ PM \_ 参数 set 请求时，微型端口驱动程序必须 \_ \_ \_ \_ 为 AP 拒绝的每个协议卸载拒绝状态指示。

例如，网络适配器可以使用 AP 的代理 ARP 来支持 ARP 卸载。

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


[**NDIS \_ PM \_ 协议 \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID \_ PM \_ 参数](./oid-pm-parameters.md)

 

