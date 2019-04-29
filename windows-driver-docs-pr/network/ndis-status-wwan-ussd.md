---
title: NDIS_STATUS_WWAN_USSD
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_USSD 通知来实现与 NDIS_WWAN_USSD_REQUEST 结构的非结构化补充服务数据 (USSD) 操作的事务完成响应。微型端口驱动程序还可以与使用 NDIS_WWAN_USSD_EVENT 结构描述 USSD 事件的性质该通知发送未经请求的事件。
ms.assetid: 6EE1235A-486E-4653-BFAC-6151C795676B
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_USSD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 27e7df1c4dc108fa526a45b7f9b3a9c034cf1dab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324877"
---
# <a name="ndisstatuswwanussd"></a>NDIS\_状态\_WWAN\_USSD


微型端口驱动程序使用 NDIS\_状态\_WWAN\_USSD 通知来实现与非结构化补充服务数据 (USSD) 操作的事务完成响应[NDIS\_WWAN\_USSD\_请求](https://msdn.microsoft.com/library/windows/hardware/hh439846)结构。

微型端口驱动程序还可以发送此通知使用未经请求的事件[NDIS\_WWAN\_USSD\_事件](https://msdn.microsoft.com/library/windows/hardware/hh439844)结构来描述 USSD 事件的性质。

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


[NDIS\_WWAN\_USSD\_REQUEST](https://msdn.microsoft.com/library/windows/hardware/hh439846)

[NDIS\_WWAN\_USSD\_EVENT](https://msdn.microsoft.com/library/windows/hardware/hh439844)

 

 




