---
title: NDIS_STATUS_LINK_STATE
description: 微型端口驱动程序使用 NDIS_STATUS_LINK_STATE 状态指示通知 NDIS 和基础驱动程序已被一个介质的物理特征中的更改。
ms.assetid: e9953fe5-68d2-47e5-aceb-b35289500262
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_LINK_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a2075a3c8677481c81fd7b9444eadda22c3f94db
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368582"
---
# <a name="ndisstatuslinkstate"></a>NDIS\_状态\_链接\_状态


微型端口驱动程序使用 NDIS\_状态\_链接\_状态状态指示通知 NDIS 和基础驱动程序已被一个介质的物理特征中的更改。

<a name="remarks"></a>备注
-------

过量驱动程序不应使用[OID\_代\_链接\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-state)OID 以确定链接状态。 而是使用 NDIS\_状态\_链接\_状态的链接状态更新的状态指示。

**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构包含[ **NDIS\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)结构。 此结构指定介质的物理的状态。

微型端口驱动程序应避免发送 NDIS\_状态\_链接\_状态状态指示，指示是否不已在该介质的物理状态中的任何更改。 但是，避免此状态指示不是一项要求。

NDIS 6.0 和更高版本的微型端口驱动程序微型端口适配器将转换为低功耗状态，如果应指示连接状态**MediaConnectStateUnknown**。 微型端口驱动程序时的微型端口适配器转换回工作电源状态，应指示的状态**MediaConnectStateConnected**经过重新建立该链接后。 NDIS 6.30 微型端口驱动程序应指示**MediaConnectStateUnknown**在低功耗转换仅当唤醒链接更改和选择性挂起时被禁用。 换言之，微型端口驱动程序必须指定的连接状态**MediaConnectStateUnknown**期间一个低能耗转换，如果无法检测和连接状态更改从低功耗状态唤醒。

NDIS 可能会向基础驱动程序传递的状态指示，如果在前面指定的链接状态为指定的链接状态中没有任何更改。 但是，不保证此行为。 过量会收到此状态指示的驱动程序必须确定哪些特征中，如果有，已更改。

如果基础驱动程序 NDIS 5。*x*或更早协议驱动程序，NDIS 转换 NDIS\_状态\_链接\_状态会向相应的 NDIS 5.1 状态指示状态指示。 NDIS 指示与更改的链接速度[ **NDIS\_状态\_链接\_速度\_更改**](ndis-status-link-speed-change.md)状态指示。 NDIS 指示中使用的连接状态的更改[ **NDIS\_状态\_媒体\_CONNECT** ](ndis-status-media-connect.md)并[ **NDIS\_状态\_媒体\_断开连接**](ndis-status-media-disconnect.md)状态指示。

NDIS 也意味着，NDIS 5。*x*过量 NDIS 6.0 和更高版本的驱动程序的微型端口驱动程序状态。 NDIS 使用状态指示或介质状态更改 NDIS 5 中标识该 NDIS。*x* OID 查询以创建 NDIS\_状态\_链接\_状态状态指示。 NDIS 执行下面的翻译：

-   [ **NDIS\_状态\_媒体\_CONNECT** ](ndis-status-media-connect.md)状态指示被转换为**MediaConnectStateConnected**中[ **NDIS\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)结构。

-   [ **NDIS\_状态\_媒体\_断开连接**](ndis-status-media-disconnect.md)状态指示被转换为**MediaConnectStateDisconnected**在中[ **NDIS\_链接\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)结构。

-   [ **NDIS\_状态\_链接\_速度\_更改**](ndis-status-link-speed-change.md)状态指示和[OID\_常规\_链接\_速度](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed)OID 用于生成链接速度状态。

有关链接状态的详细信息，请参阅[OID\_代\_链接\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-state)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_LINK\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_link_state)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[**NDIS\_状态\_链接\_速度\_更改**](ndis-status-link-speed-change.md)

[**NDIS\_状态\_媒体\_连接**](ndis-status-media-connect.md)

[**NDIS\_状态\_媒体\_断开连接**](ndis-status-media-disconnect.md)

[OID\_GEN\_LINK\_SPEED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed)

[OID\_GEN\_LINK\_STATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-state)

 

 




