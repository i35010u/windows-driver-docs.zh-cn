---
title: OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS
description: OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 用于设置或查询首选多运营商网络提供商的列表。 多运营商提供商是指可以设置为 home 提供商的提供商。
ms.assetid: BA78E0B9-1B57-412C-83E7-328F8304C82D
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 43f87b7a2173dabb20661ed5aea1aa5599b577b5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843812"
---
# <a name="oid_wwan_preferred_multicarrier_providers"></a>OID\_WWAN\_首选\_多\_提供程序


OID\_WWAN\_首选\_多\_提供程序用于*设置*或*查询*首选多运营商网络提供商的列表。 多运营商提供商是指可以*设置*为 home 提供商的提供商。

支持*set*和*query*请求。 微型端口驱动程序必须异步处理*集*和*查询*请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后发送[**ndis\_状态\_wwan\_首选\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers) [ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)\_\_\_

当响应\_WWAN\_首选\_提供程序*查询*请求时，微型端口驱动程序应将**PreferredListHeader**成员设置为**WwanStructProvider2** ，并将**PreferredListHeader**成员设置为列表中的提供程序数。 *查询*中返回的多运营商提供程序必须能够在首选多运营商列表返回到服务时设置为主提供商。

当响应 OID\_WWAN\_首选\_提供程序*设置*请求时，微型端口驱动程序应将**PreferredListHeader**成员**设置为0，并将** **PreferredListHeader**成员设置为0。

出现错误时，微型端口应将 NDIS 的**uStatus**成员设置\_WWAN\_首选\_多\_提供程序结构，并将**PreferredListHeader** **和 elementcount 多于设置为** **PreferredListHeader**。

WWAN\_PROVIDER2 结构的**Rssi**和**ErrorRate**成员应设置为（如果可用）。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_首选\_多\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)

[ **\_WWAN\_首选\_多\_提供程序的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-preferred-multicarrier-providers)

[MB 提供程序操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-provider-operations)

 

 




