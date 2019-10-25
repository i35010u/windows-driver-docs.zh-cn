---
title: NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 通知来响应以前的 OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERSquery 请求。小型端口驱动程序还可以使用此通知来通知 MB 服务有关更新的信息，这是由于来自 MB 服务的 OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 集请求引起的。 OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 集请求的响应在 PreferredListHeader 成员中必须包含零个元素。 小型端口驱动程序还可以通过此通知发送未经请求的事件，以通知 MB 服务首选的多运营商提供程序列表（PMCPL）已更改。此通知使用 NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 结构。
ms.assetid: DBE8911D-1A92-40BC-94EB-BED3B8B82CB0
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d5ec5345a77efbcc88edd9d7d82e988e9f69dc71
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844700"
---
# <a name="ndis_status_wwan_preferred_multicarrier_providers"></a>\_WWAN\_首选\_多\_提供程序的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_首选\_多\_提供程序通知以响应以前的[OID\_WWAN\_首选\_多\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-multicarrier-providers)*查询*请求。

如果 OID\_WWAN\_首选\_多\_提供程序从 MB 服务中*设置*请求，则微型端口驱动程序还可能使用此通知来通知 MB 服务有关更新的信息。 对\_WWAN\_首选\_多\_提供程序*集*请求的 OID 的响应在**PreferredListHeader**成员中必须包含零个元素。 小型端口驱动程序还可以通过此通知发送未经请求的事件，以通知 MB 服务首选的多运营商提供程序列表（PMCPL）已更改。

此通知使用[**NDIS\_WWAN\_首选\_多\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)结构。

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

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_首选\_多\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)

 

 




