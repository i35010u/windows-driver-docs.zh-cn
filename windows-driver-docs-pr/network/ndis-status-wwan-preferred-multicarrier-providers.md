---
title: NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 通知对上一个 OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERSquery 请求作出响应。微型端口驱动程序还可以使用此通知来通知有关从 MB 服务 OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 集请求的结果更新 MB 服务。 OID_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 集请求的响应必须包含 PreferredListHeader 成员中的零个元素。 微型端口驱动程序还可以发送此通知来通知首选多运营商提供程序列表 (PMCPL) 已更改 MB 服务的未经请求的事件。此通知使用 NDIS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 结构。
ms.assetid: DBE8911D-1A92-40BC-94EB-BED3B8B82CB0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_PREFERRED_MULTICARRIER_PROVIDERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 572e9df0ab54f193497ebb3ad19a50f01edcc106
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377597"
---
# <a name="ndisstatuswwanpreferredmulticarrierproviders"></a>NDIS\_状态\_WWAN\_PREFERRED\_多\_提供程序


微型端口驱动程序使用 NDIS\_状态\_WWAN\_PREFERRED\_多\_提供程序通知，可以对上一次响应[OID\_WWAN\_首选\_多\_提供程序](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-preferred-multicarrier-providers)*查询*请求。

微型端口驱动程序还可以使用此通知来告知由于 OID 更新 MB 服务\_WWAN\_PREFERRED\_多\_提供程序*设置*从请求MB 服务。 对 OID 的响应\_WWAN\_PREFERRED\_多\_提供程序*设置*请求必须包含零个元素中的**PreferredListHeader**成员。 微型端口驱动程序还可以发送此通知来通知首选多运营商提供程序列表 (PMCPL) 已更改 MB 服务的未经请求的事件。

使用此通知[ **NDIS\_WWAN\_首选\_多\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)结构。

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
<td><p>支持从 Windows 8 开始。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_PREFERRED\_多\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_preferred_multicarrier_providers)

 

 




