---
title: NDIS_STATUS_WWAN_USSD
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_USSD 通知来实现使用 NDIS_WWAN_USSD_REQUEST 结构 (USSD) 操作的非结构化补充服务数据的事务完成响应。小型端口驱动程序还可以使用 NDIS_WWAN_USSD_EVENT 结构通过此通知发送未经请求的事件，以描述 USSD 事件的性质。
ms.assetid: 6EE1235A-486E-4653-BFAC-6151C795676B
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_USSD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a209a1a904c7a94f2d5e51bf19c5e1426b91f865
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218402"
---
# <a name="ndis_status_wwan_ussd"></a>NDIS \_ 状态 \_ WWAN \_ USSD


微型端口驱动程序使用 NDIS \_ 状态 \_ WWAN \_ USSD 通知，为非结构化补充服务数据 (USSD) 操作与 [NDIS \_ WWAN \_ USSD \_ 请求](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_request) 结构实现事务完成响应。

小型端口驱动程序还可以使用 [NDIS \_ WWAN \_ USSD \_ 事件](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event) 结构通过此通知发送未经请求的事件，以描述 USSD 事件的性质。

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


[NDIS \_ WWAN \_ USSD \_ 请求](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_request)

[NDIS \_ WWAN \_ USSD \_ 事件](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_ussd_event)

 

