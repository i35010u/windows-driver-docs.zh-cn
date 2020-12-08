---
title: NDIS_STATUS_WWAN_PREFERRED_PROVIDERS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PREFERRED_PROVIDERS 通知来通知 MB 服务 (PPL) 的首选提供程序列表已更改。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_PREFERRED_PROVIDERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7c4b8d5af90b458383390dc38248e27eba02b839
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838741"
---
# <a name="ndis_status_wwan_preferred_providers"></a>NDIS \_ 状态 \_ WWAN \_ 首选 \_ 提供程序


微型端口驱动程序使用 NDIS \_ 状态 \_ WWAN \_ 首选 \_ 提供程序通知来通知 MB 服务 (PPL) 的首选提供程序列表已更改。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ 首选 \_ 提供程序**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers) 结构。

<a name="remarks"></a>备注
-------

在某些情况下，基于 GSM 的设备的 PPL () 由网络通过无线 (OTA) 或短消息服务 (SMS) 进行更新。 微型端口驱动程序必须相应地更新 PPL。 之后，小型端口驱动程序必须使用这一指示和更新的 PPL 通知 MB 服务有关更新的信息。 对于基于 GSM 的网络，NDIS **PreferredListHeader** \_ WWAN \_ 首选 \_ 提供程序结构的 PreferredListHeader 成员必须指向更新的 PPL。

微型端口驱动程序使用这一指示，通过 [OID \_ WWAN \_ 首选 \_ 提供程序](oid-wwan-preferred-providers.md) 从 mb 服务中设置请求，通知 MB 服务有关更新。 对 OID \_ WWAN \_ 首选 \_ 提供程序集请求的响应在 **PreferredListHeader** 成员中必须包含零个元素。

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
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ WWAN \_ 首选 \_ 提供程序**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)

[OID \_ WWAN \_ 首选 \_ 提供程序](oid-wwan-preferred-providers.md)

 

