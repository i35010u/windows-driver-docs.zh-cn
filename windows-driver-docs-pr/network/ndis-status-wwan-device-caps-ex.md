---
title: NDIS_STATUS_WWAN_DEVICE_CAPS_EX
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_CAPS_EX 通知来告知 MB 服务关于完成的上一个 OID_WWAN_DEVICE_CAPS_EX 查询请求。
ms.assetid: 7E596CB0-2A08-45E4-9932-5E951B880D62
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_CAPS_EX 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a27e48a081a967e87c3f375cacbed14e1b8a0f6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375178"
---
# <a name="ndisstatuswwandevicecapsex"></a>NDIS\_STATUS\_WWAN\_DEVICE\_CAPS\_EX


微型端口驱动程序使用**NDIS\_状态\_WWAN\_设备\_CAPS\_EX**通知来通知关于完成的上一MB服务[OID\_WWAN\_设备\_CAP\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps-ex)查询请求。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_设备\_CAPS\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)结构。

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
<td><p>Windows 10，版本 1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WWAN\_DEVICE\_CAPS\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps-ex)

[**NDIS\_WWAN\_DEVICE\_CAPS\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)

 

 




