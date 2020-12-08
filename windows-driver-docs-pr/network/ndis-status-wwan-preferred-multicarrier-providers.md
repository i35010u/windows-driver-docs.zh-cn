---
title: NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 通知来响应以前的 OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERSquery 请求。小型端口驱动程序还可以使用此通知来通知 MB 服务有关更新的信息，这是由于来自 MB 服务的 OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 设置请求引起的。 对 OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 集请求的响应在 PreferredListHeader 成员中必须包含零个元素。 小型端口驱动程序还可以通过此通知发送未经请求的事件，以通知 MB 服务 (PMCPL) 的首选多运营商提供程序列表已更改。此通知使用 NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 结构。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9e95b8a79fd6b593ded68b15e9b391419df9ef4a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794351"
---
# <a name="ndis_status_wwan_preferred_multicarrier_providers"></a>NDIS \_ 状态 \_ WWAN \_ 首选 \_ 多 \_ 提供程序


微型端口驱动程序使用 NDIS \_ 状态 \_ wwan \_ 首选 \_ 多 \_ 提供程序通知来响应以前的 [OID \_ wwan \_ 首选 \_ 多 \_ 提供程序](./oid-wwan-preferred-multicarrier-providers.md)*查询* 请求。

小型端口驱动程序还可以使用此通知来通知 MB 服务有关更新的信息，这是由 OID \_ WWAN \_ 首选 \_ 多 \_ 提供程序从 MB 服务发出的。 *set* 对 OID \_ WWAN \_ 首选 \_ 多 \_ 提供程序 *集* 请求的响应在 **PreferredListHeader** 成员中必须包含零个元素。 小型端口驱动程序还可以通过此通知发送未经请求的事件，以通知 MB 服务 (PMCPL) 的首选多运营商提供程序列表已更改。

此通知使用 [**NDIS \_ WWAN \_ 首选 \_ 多 \_ 提供程序**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers) 结构。

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
<td><p>从 Windows 8 开始支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ WWAN \_ 首选 \_ 多 \_ 提供程序**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)

 

