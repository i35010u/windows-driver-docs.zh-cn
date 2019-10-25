---
title: NDIS_STATUS_PM_WOL_PATTERN_REJECTED
description: NDIS_STATUS_PM_WOL_PATTERN_REJECTED 状态指示过量驱动程序已拒绝电源管理唤醒（WOL）模式。
ms.assetid: 49180c69-a3b8-4a6f-b34f-93e063c88f43
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_PM_WOL_PATTERN_REJECTED 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c03d74ba9fd8c956ef0d3bfb5fc28930b36cd945
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843534"
---
# <a name="ndis_status_pm_wol_pattern_rejected"></a>NDIS\_状态\_PM\_WOL\_模式\_被拒绝


NDIS\_状态\_PM\_WOL\_模式\_拒绝状态指示过量驱动程序已拒绝电源管理唤醒（WOL）模式。

<a name="remarks"></a>备注
-------

当任何一个删除 WOL 模式时，NDIS 或微型端口驱动程序都可以生成 NDIS\_状态\_PM\_WOL\_模式\_拒绝的状态指示。 [**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含被拒绝的 wol 模式的 WOL 模式标识符的 ULONG。 NDIS 在[**ndis\_PM\_wol\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)结构的**PatternId**成员中提供了 wol 模式标识符。

当必须从网络适配器中删除以前添加的 WOL 模式时，NDIS\_状态\_PM\_WOL\_模式\_拒绝的状态指示。 例如，对于更高优先级的 WOL 模式，NDIS 可能会删除 WOL 模式以释放资源。 通知事件将仅发送到添加了删除模式的绑定。

对于使用基础结构元素跨基础结构分担模式和漫游的无线网络适配器，可能新的基础结构元素可能不支持与上一元素相同的功能。 在这种情况下，微型端口驱动程序可以向 NDIS 发出状态指示，NDIS 将\_PM 发出 NDIS\_状态，\_WOL\_模式\_拒绝了特定错误代码。

WiFi 驱动程序可能会在本地缓存唤醒模式。 当驱动程序处理 OID 以添加或删除唤醒模式时，驱动程序可以选择仅更新其本地缓存。 驱动程序可以将基础结构的更新推迟到[\_PM\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)OID 接收到 oid 之后。

基础结构可能没有足够的资源来容纳所有唤醒模式。 在这种情况下，基础结构可以接受唤醒模式的部分列表。 当微型端口驱动程序完成 OID\_PM\_参数设置请求时，驱动程序必须将 NDIS\_状态\_PM\_WOL\_模式\_拒绝访问点（AP）拒绝。

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


[**NDIS\_PM\_WOL\_模式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_wol_pattern)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_PM\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-parameters)

 

 




