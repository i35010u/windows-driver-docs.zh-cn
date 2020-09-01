---
title: NDIS_STATUS_LINK_STATE
description: 微型端口驱动程序使用 NDIS_STATUS_LINK_STATE 状态指示来通知 NDIS 和过量驱动程序的物理特性发生了变化。
ms.assetid: e9953fe5-68d2-47e5-aceb-b35289500262
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_LINK_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: eda585f786bbfde4b50c1412e9648f76ac0f9ab2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211745"
---
# <a name="ndis_status_link_state"></a>NDIS \_ 状态 \_ 链接 \_ 状态


微型端口驱动程序使用 NDIS \_ 状态 \_ 链接 \_ 状态指示来通知 ndis 和过量驱动程序，这种情况已改变了中型的物理特性。

<a name="remarks"></a>备注
-------

过量驱动程序不应使用 [OID \_ 生成 \_ 链接 \_ 状态](./oid-gen-link-state.md) oid 来确定链接状态。 相反，请使用 NDIS \_ 状态 \_ 链接 \_ 状态指示进行链接状态更新。

[**Ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含[**ndis \_ 链接 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构。 此结构指定介质的物理状态。

如果介质的物理状态没有变化，微型端口驱动程序应避免发送 NDIS \_ 状态 \_ 链接 \_ 状态指示。 但是，不要求避免此状态指示。

如果微型端口适配器转换为低功率状态，NDIS 6.0 和更高版本的微型端口驱动程序应指示连接状态为 " **MediaConnectStateUnknown**"。 当微型端口适配器转换回工作电源状态时，微型端口驱动程序应在重新建立链接后指示 **MediaConnectStateConnected** 的状态。 仅当禁用了唤醒链接更改和选择性挂起功能时，NDIS 6.30 微型端口驱动程序才应指示 **MediaConnectStateUnknown** 。 换而言之，如果无法检测并唤醒连接状态更改（从低功耗状态更改），微型端口驱动程序必须指示 **MediaConnectStateUnknown** 的连接状态。

如果在前面指示的链接状态中指定的链接状态不存在更改，NDIS 可能不会向过量驱动程序传递状态指示。 但是，这种行为并不保证。 收到此状态指示的过量驱动程序必须确定介质（如果有）的哪些特征发生了更改。

如果过量驱动程序是 NDIS 5，则为。*x* 或更早的协议驱动程序，ndis 会将 ndis \_ 状态 \_ 链接 \_ 状态指示转换为相应的 ndis 5.1 状态指示。 NDIS 指示链接速度更改，并显示 [**NDIS \_ 状态 \_ 链接 \_ 速度 \_ 更改**](ndis-status-link-speed-change.md) 状态指示。 NDIS 指示连接状态发生更改，并显示 [**ndis \_ 状态 \_ Media \_ CONNECT**](ndis-status-media-connect.md) 和 [**ndis \_ 状态 \_ 媒体 \_ 断开**](ndis-status-media-disconnect.md) 连接状态指示。

NDIS 还会转换 NDIS 5。用于过量 NDIS 6.0 和更高版本驱动程序的*x* 微型端口驱动程序状态。 Ndis 使用 ndis 5 中标识的状态指示或媒体状态更改。*x* OID 查询，用于创建 NDIS \_ 状态 \_ 链接 \_ 状态状态指示。 NDIS 执行以下转换：

-   [**Ndis \_ 状态 \_ 媒体 \_ 连接**](ndis-status-media-connect.md)状态指示转换为[**Ndis \_ 链接 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构中的**MediaConnectStateConnected** 。

-   [**Ndis \_ 状态 \_ 媒体 \_ 断开连接**](ndis-status-media-disconnect.md)状态指示转换为[**Ndis \_ 链接 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)结构中的**MediaConnectStateDisconnected** 。

-   [**NDIS \_ 状态 \_ 链接 \_ 速度 \_ 更改**](ndis-status-link-speed-change.md)状态指示和 oid 生成[ \_ \_ 链接 \_ 速度](./oid-gen-link-speed.md)oid 用于生成链接速度状态。

有关链接状态的详细信息，请参阅 [OID \_ GEN \_ 链接 \_ 状态](./oid-gen-link-state.md)。

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
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ 链接 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_link_state)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[**NDIS \_ 状态 \_ 链接 \_ 速度 \_ 更改**](ndis-status-link-speed-change.md)

[**NDIS \_ 状态 \_ 媒体 \_ 连接**](ndis-status-media-connect.md)

[**NDIS \_ 状态 \_ 媒体 \_ 断开连接**](ndis-status-media-disconnect.md)

[OID \_ GEN \_ LINK \_ 速度](./oid-gen-link-speed.md)

[OID \_ 生成 \_ 链接 \_ 状态](./oid-gen-link-state.md)

 

