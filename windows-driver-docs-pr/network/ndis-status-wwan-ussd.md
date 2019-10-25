---
title: NDIS_STATUS_WWAN_USSD
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_USSD 通知为具有 NDIS_WWAN_USSD_REQUEST 结构的非结构化补充服务数据（USSD）操作实现事务完成响应。小型端口驱动程序还可以使用 NDIS_WWAN_USSD_EVENT 结构通过此通知发送未经请求的事件，以描述 USSD 事件的性质。
ms.assetid: 6EE1235A-486E-4653-BFAC-6151C795676B
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_USSD 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3a7a30778d728f59e9bc2659a50d4d9ab63a22af
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834660"
---
# <a name="ndis_status_wwan_ussd"></a>WWAN\_USSD\_NDIS\_状态


微型端口驱动程序使用 NDIS\_状态\_WWAN\_USSD 通知来实现使用[ndis\_WWAN\_USSD 实现的非结构化补充服务数据（USSD）操作的事务完成响应\_请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_request)结构。

小型端口驱动程序还可以使用[NDIS\_WWAN\_USSD\_事件](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event)结构来说明 USSD 事件的性质，以此通知发送未经请求的事件。

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


[NDIS\_WWAN\_USSD\_请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_request)

[NDIS\_WWAN\_USSD\_事件](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event)

 

 




