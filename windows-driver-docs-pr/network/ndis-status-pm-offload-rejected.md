---
title: NDIS_STATUS_PM_OFFLOAD_REJECTED
description: NDIS_STATUS_PM_OFFLOAD_REJECTED 状态向过量驱动程序指示电源管理协议卸载已被拒绝。
ms.assetid: 54922e70-2b56-4141-b79b-73418c7553e3
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_OFFLOAD_REJECTED 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 4bc9ac0203c8578492d1590895d2c50de82a42cc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843537"
---
# <a name="ndis_status_pm_offload_rejected"></a>\_PM\_卸载\_拒绝的 NDIS\_状态


NDIS\_状态\_PM\_卸载\_拒绝的状态表明已拒绝电源管理协议卸载的过量驱动程序。

<a name="remarks"></a>备注
-------

NDIS 或微型端口驱动程序可以生成 NDIS\_状态\_PM\_卸载\_拒绝状态指示，这两个状态都会删除卸载的协议。 [**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含用于已拒绝协议卸载的协议卸载标识符的 ULONG。 NDIS 在 Ndis\_PM 的**ProtocolOffloadId**成员中提供了协议卸载标识符[ **\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构。

当必须从网络适配器中删除以前卸载的协议时，NDIS\_状态\_PM\_卸载\_拒绝状态指示。 例如，对于更高优先级的协议卸载，NDIS 可能会删除协议卸载以释放资源。 NDIS 将状态指示发送到卸载被拒绝的协议卸载的绑定，但不会将其发送到其他绑定。

微型端口驱动程序报告此状态指示以拒绝先前接受的协议卸载。 例如，对于 WiFi WOL 事例，微型端口驱动程序必须将 NDIS\_状态设置\_PM\_卸载\_在不需要 PTK/GTK 旋转（由于供应商特定基础结构支持）时拒绝状态指示。

对于使用基础结构元素跨基础结构卸载协议和漫游的无线网络适配器，可能新的基础结构元素可能不支持与上一元素相同的功能。 在这种情况下，微型端口驱动程序可以向 NDIS 发出状态指示，并且 NDIS 将发出 NDIS\_状态\_PM\_卸载\_拒绝特定的错误代码。

WiFi 驱动程序可以在本地缓存协议卸载请求。 当驱动程序处理 OID 以添加或删除协议卸载时，驱动程序可以选择仅更新其本地缓存。 驱动程序可以将基础结构的更新推迟到[\_PM\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)OID 接收到 oid 之后。

基础结构可能没有足够的资源来容纳所有协议卸载。 在这种情况下，基础结构可以接受部分协议卸载。 当微型端口驱动程序完成 OID\_PM\_参数设置请求时，微型端口驱动程序必须\_PM 使 NDIS\_状态\_卸载\_拒绝了 AP 的每个协议的状态指示拒收.

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
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_PM\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)

 

 




