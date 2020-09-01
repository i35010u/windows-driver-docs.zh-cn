---
title: OID_WWAN_VISIBLE_PROVIDERS
description: OID_WWAN_VISIBLE_PROVIDERS 返回当前在 MB 设备范围内可见的网络提供程序列表。
ms.assetid: 4dfd4477-6332-4163-8b3e-a1604b11d175
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_VISIBLE_PROVIDERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f308d3a5a6acd184b5971320119a704eff0c379d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206295"
---
# <a name="oid_wwan_visible_providers"></a>OID \_ WWAN \_ 可见 \_ 提供程序


OID \_ WWAN \_ 可见 \_ 提供程序返回当前在 MB 设备范围内可见的网络提供程序列表。

不支持设置请求。

微型端口驱动程序必须异步处理查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 " \_ wwan 可见提供 \_ \_ 程序**](ndis-status-wwan-visible-providers.md) 状态通知"，其中包含 [**ndis \_ WWAN \_ 可见 \_ 提供**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers) 程序的状态通知，以提供有关完成查询请求时可见网络提供程序的信息。

*查询* 请求将 NDIS \_ WWAN \_ GET \_ VISIBLE \_ PROVIDERS 结构指定为输入。 如果将**Action** wwan \_ 获取可见提供程序中的操作成员 \_ \_ 设置为 wwan \_ 获取 \_ 可见提供程序，则 \_ \_ 所有微型端口都应返回所有可见的提供程序。 如果将**Action** wwan \_ 获取可见提供程序中的操作成员 \_ \_ 设置为 wwan \_ 获取 \_ 可见提供程序多， \_ \_ 微型端口应只返回可以设置为 home 提供程序的可见多运营商提供程序。

设备返回的可见提供程序列表应为每个提供程序正确设置提供程序状态。 例如，应将多首选提供程序标记为 WWAN \_ 提供程序 \_ 状态 \_ 首选 \_ 多，当前的 home 提供程序（如果有任何标记为 wwan \_ 提供程序 \_ 状态 \_ home），当前的已注册提供程序（如果有）应标记为 wwan \_ 提供程序 \_ 状态 \_ 。

WWAN PROVIDER2 结构的 **Rssi** 和 **ErrorRate** 成员 \_ 应设置为（如果可用）。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [WWAN 提供程序操作](./mb-provider-operations.md)。

当处理查询操作时，微型端口驱动程序可以 (SIM 卡) 访问订阅服务器标识模块，但不应访问提供程序网络。

微型端口驱动程序应将 **VisibleListHeader** 成员设置为 *WwanStructProvider*。

对于基于 CDMA 的网络，微型端口驱动程序应仅返回 home 提供程序，如果首选漫游列表中的任何网络 (PRL) 当前都可见。 对于基于 GSM 的网络，可见提供程序列表中可能会出现多个提供程序。

如果设备在连接时不支持对可见提供程序进行扫描，则 \_ 应 \_ 在 NDIS **uStatus** \_ WWAN \_ 可见 \_ 提供程序结构的 uStatus 成员中返回 WWAN 状态繁忙错误值。

在注册模式下，基于 GSM 和 CDMA 的设备必须支持扫描可见提供程序。 但是，无需使用微型端口驱动程序来支持扫描可见提供程序，同时 (PDP) 上下文处于活动状态 (，例如，设备已连接到提供商的网络) 。

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

## <a name="see-also"></a>另请参阅


[**NDIS \_ WWAN \_ 可见 \_ 提供程序**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_visible_providers)

[**NDIS \_ 状态 \_ WWAN \_ 可见 \_ 提供程序**](ndis-status-wwan-visible-providers.md)

[WWAN 提供程序操作](./mb-provider-operations.md)

 

