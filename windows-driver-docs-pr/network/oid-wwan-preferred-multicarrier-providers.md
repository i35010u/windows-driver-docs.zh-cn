---
title: OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS
description: OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 用于设置或查询首选多运营商网络提供商的列表。 多运营商提供商是指可以设置为 home 提供商的提供商。
ms.assetid: BA78E0B9-1B57-412C-83E7-328F8304C82D
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ae0e54dd8f93310e95cc41f989b856f14145411d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216136"
---
# <a name="oid_wwan_preferred_multicarrier_providers"></a>OID \_ WWAN \_ 首选 \_ 多 \_ 提供程序


OID \_ WWAN \_ 首选 \_ 多 \_ 提供程序用于 *设置* 或 *查询* 首选多运营商网络提供商的列表。 多运营商提供商是指可以 *设置* 为 home 提供商的提供商。

支持 *set* 和 *query* 请求。 微型端口驱动程序必须异步处理 *集* 和 *查询* 请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 \_ WWAN \_ 首选 \_ 多 \_ 提供程序**](./ndis-status-wwan-preferred-multicarrier-providers.md) 状态通知，其中包含 [**ndis \_ WWAN \_ 首选 \_ 多 \_ 提供程序**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers) 结构。

当响应 OID **PreferredListHeader.ElementType** WWAN **WwanStructProvider2** **PreferredListHeader.ElementCount** \_ \_ 首选 \_ 提供程序*查询*请求时，微型端口驱动程序应将 PreferredListHeader 成员设置为 WwanStructProvider2，并将 PreferredListHeader 成员设置为列表中的提供程序数。 *查询*中返回的多运营商提供程序必须能够在首选多运营商列表返回到服务时设置为主提供商。

当响应 OID **PreferredListHeader.ElementType** WWAN **PreferredListHeader.ElementCount**首选**WwanStructProvider2** \_ \_ \_ 提供程序*集*请求时，微型端口驱动程序应将 PreferredListHeader 成员设置为0，并将 PreferredListHeader 成员设置为0。

出现错误时，微型端口应**uStatus**将 NDIS \_ WWAN \_ 首选多提供程序结构的 uStatus 成员设置为失败状态，将 PreferredListHeader 设置为 elementcount 多于，将 \_ \_ **PreferredListHeader**设置为**WwanStructProvider2**。 **PreferredListHeader.ElementCount**

WWAN PROVIDER2 结构的 **Rssi** 和 **ErrorRate** 成员 \_ 应设置为（如果可用）。

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
<td><p>版本：在 windows 8 及更高版本的 Windows 中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ WWAN \_ 首选 \_ 多 \_ 提供程序**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)

[**NDIS \_ 状态 \_ WWAN \_ 首选 \_ 多 \_ 提供程序**](./ndis-status-wwan-preferred-multicarrier-providers.md)

[MB 提供程序操作](./mb-provider-operations.md)

 

