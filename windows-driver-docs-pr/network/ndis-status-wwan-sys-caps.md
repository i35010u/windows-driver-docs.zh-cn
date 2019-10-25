---
title: NDIS_STATUS_WWAN_SYS_CAPS_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SYS_CAPS_INFO 通知来通知 MB 服务完成了以前的 OID_WWAN_SYS_CAPS_INFO 查询请求。
ms.assetid: 653A35EC-29BB-458D-B33C-41EF6EF47A6E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_SYS_CAPS_INFO 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 18a02c8404785648f903de3555bb239fc23f82e6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844626"
---
# <a name="ndis_status_wwan_sys_caps_info"></a>NDIS\_状态\_WWAN\_SYS\_CAP\_信息


微型端口驱动程序使用**NDIS\_状态\_WWAN\_SYS\_cap\_info**通知，通知 MB 服务有关上一个 OID 的完成[\_WWAN\_sys.databases](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sys-caps)\_查询请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_SYS\_cap\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)结构。

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


[OID\_WWAN\_SYS\_CAP\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sys-caps)

[**NDIS\_WWAN\_SYS\_CAP\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sys_caps_info)

 

 




