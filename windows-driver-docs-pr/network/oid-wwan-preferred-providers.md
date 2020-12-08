---
title: OID_WWAN_PREFERRED_PROVIDERS
description: OID_WWAN_PREFERRED_PROVIDERS 返回有关基于 GSM 的设备的首选提供程序列表的信息。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PREFERRED_PROVIDERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 27c9063776b6055ff9866fefce4806a60df09699
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793427"
---
# <a name="oid_wwan_preferred_providers"></a>OID \_ WWAN \_ 首选 \_ 提供程序


OID \_ WWAN \_ 首选 \_ 提供程序返回有关基于 GSM 的设备的首选提供程序列表的信息。 基于 CDMA 的设备的微型端口驱动程序无需支持此 OID。

微型端口驱动程序必须异步处理集和查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 \_ WWAN \_ 首选 \_ 提供**](ndis-status-wwan-preferred-providers.md) 程序状态通知，其中包含 [**ndis \_ WWAN \_ 首选 \_**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers) 提供程序结构，以提供有关 (PPL) 的首选提供程序列表的信息，而不考虑完成集或查询请求。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [WWAN 提供程序操作](./mb-provider-operations.md)。

当处理查询请求时，微型端口驱动程序可以 (SIM 卡) 访问订阅服务器标识模块，但不应访问提供程序网络。

当处理设置请求时，微型端口驱动程序可以 (SIM 卡) 或提供程序网络访问订阅服务器标识模块。

处理 OID \_ WWAN \_ 首选 \_ 提供程序时，微型端口驱动程序可能只设置 wwan \_ 提供程序 \_ 状态 \_ 首选或 wwan \_ 提供程序 \_ 状态 \_ 禁止标志来标记列表项。 请注意，对于基于 GSM 的设备，禁止的访问接口可能不会出现在列表中。

微型端口 driverrs 应将 **PreferredListHeader** 成员设置为 *WwanStructProvider*。 当响应 OID **PreferredListHeader.ElementCount** \_ WWAN \_ 首选 \_ 提供程序集请求时，微型端口驱动程序应将 PreferredListHeader 成员设置为0。

处理设置请求时是否可以覆盖设备上的 PPL 取决于设备功能、移动电话技术和/或网络提供商的策略。

如果微型端口驱动程序 \_ 不 \_ \_ 支持返回或设置 PPL，则它应返回不受支持的 NDIS 状态。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ WWAN \_ 首选 \_ 提供程序**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)

[**NDIS \_ 状态 \_ WWAN \_ 首选 \_ 提供程序**](ndis-status-wwan-preferred-providers.md)

[WWAN 提供程序操作](./mb-provider-operations.md)

 

