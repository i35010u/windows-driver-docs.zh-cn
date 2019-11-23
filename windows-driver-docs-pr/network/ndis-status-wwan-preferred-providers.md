---
title: NDIS_STATUS_WWAN_PREFERRED_PROVIDERS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PREFERRED_PROVIDERS 通知来通知 MB 服务，首选提供程序列表（PPL）已更改。
ms.assetid: b0c06db9-82ca-4f94-80e6-3cf13197abf5
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_PREFERRED_PROVIDERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ef3a982061a1ddd75c3aca9d7d669c3bd091e766
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844697"
---
# <a name="ndis_status_wwan_preferred_providers"></a>\_WWAN\_首选\_提供程序的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_首选的\_提供程序通知来通知 MB 服务，首选提供程序列表（PPL）已更改。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_首选\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)结构。

<a name="remarks"></a>备注
-------

在某些情况下，PPL （对于基于 GSM 的设备）由网络通过无线（OTA）或短信服务（SMS）进行更新。 微型端口驱动程序必须相应地更新 PPL。 之后，小型端口驱动程序必须使用这一指示和更新的 PPL 通知 MB 服务有关更新的信息。 对于基于 GSM 的网络，NDIS\_WWAN\_首选\_提供程序结构的**PreferredListHeader**成员必须指向更新的 PPL。

微型端口驱动程序使用这一指示，通过[OID\_WWAN\_首选\_提供程序](oid-wwan-preferred-providers.md) 从 MB 服务请求设置请求，通知 MB 服务。 对\_WWAN\_首选\_提供程序集请求的 OID 的响应在**PreferredListHeader**成员中必须包含零个元素。

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

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_首选\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_providers)

[OID\_WWAN\_首选\_提供程序](oid-wwan-preferred-providers.md)

 

 




