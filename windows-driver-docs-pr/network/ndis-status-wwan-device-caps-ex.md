---
title: NDIS_STATUS_WWAN_DEVICE_CAPS_EX
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_CAPS_EX 通知来通知 MB 服务完成了以前的 OID_WWAN_DEVICE_CAPS_EX 查询请求。
ms.assetid: 7E596CB0-2A08-45E4-9932-5E951B880D62
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_CAPS_EX 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3f34c809354df387c1a56bcb8b02df4991d4e40d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842649"
---
# <a name="ndis_status_wwan_device_caps_ex"></a>\_WWAN\_设备\_CAP 的 NDIS\_状态\_EX


微型端口驱动程序使用**NDIS\_状态\_WWAN\_设备\_cap\_ex**通知来通知 MB 服务完成以前 OID 的完成[\_WWAN\_设备\_\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps-ex)查询请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_设备\_cap\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)结构。

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
<td><p>Windows 10 版本1703</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_设备\_CAP\_EX](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps-ex)

[**NDIS\_WWAN\_设备\_CAP\_EX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_caps_ex)

 

 




